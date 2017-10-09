---
title: "Настройка принудительного туннелирования для подключений типа \"сеть — сеть\" Azure (классическая модель) | Документация Майкрософт"
description: "Как tooredirect или «принудительно» все tooyour назад Интернета трафик локального расположения."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a><span data-ttu-id="46eac-103">Настройка принудительного туннелирования с помощью hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="46eac-103">Configure forced tunneling using hello classic deployment model</span></span>

<span data-ttu-id="46eac-104">Принудительное туннелирование позволяет перенаправлять или «принудительно» все в локальное расположение задней tooyour Интернета трафик через туннель VPN сайт-сайт для проверки и аудита.</span><span class="sxs-lookup"><span data-stu-id="46eac-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="46eac-105">Это критически важное требование безопасности, имеющееся в большинстве корпоративных ИТ-политик.</span><span class="sxs-lookup"><span data-stu-id="46eac-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="46eac-106">Без принудительного туннелирования Интернет-трафик из виртуальных машин в Azure будет всегда проходить из сетевой инфраструктуры Azure непосредственно из toohello Интернета, без параметра tooallow hello вы tooinspect или аудита hello трафика.</span><span class="sxs-lookup"><span data-stu-id="46eac-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="46eac-107">Несанкционированный доступ через Интернет потенциально может привести tooinformation раскрытию или другие виды угроз безопасности.</span><span class="sxs-lookup"><span data-stu-id="46eac-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="46eac-108">В этой статье описывается настройка принудительного туннелирования для виртуальных сетей, созданных с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="46eac-108">This article walks you through configuring forced tunneling for virtual networks created using hello classic deployment model.</span></span> <span data-ttu-id="46eac-109">Принудительное туннелирование можно настроить с помощью PowerShell, не через портал hello.</span><span class="sxs-lookup"><span data-stu-id="46eac-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="46eac-110">Tooconfigure принудительного туннелирования для модели развертывания диспетчера ресурсов hello из hello, следуя раскрывающегося списка выберите классический статьи:</span><span class="sxs-lookup"><span data-stu-id="46eac-110">If you want tooconfigure forced tunneling for hello Resource Manager deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="46eac-111">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="46eac-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="46eac-112">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="46eac-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="46eac-113">Требования и рекомендации</span><span class="sxs-lookup"><span data-stu-id="46eac-113">Requirements and considerations</span></span>
<span data-ttu-id="46eac-114">В Azure принудительное туннелирование настраивается с помощью определяемых пользователем маршрутов виртуальной сети (UDR).</span><span class="sxs-lookup"><span data-stu-id="46eac-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="46eac-115">Перенаправление трафика tooan из локального сайта выражается как шлюз Azure VPN toohello маршрут по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="46eac-115">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="46eac-116">Hello следующем разделе перечислены hello текущее ограничение таблицы маршрутизации hello и маршрутов для виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="46eac-116">hello following section lists hello current limitation of hello routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="46eac-117">Каждая подсеть виртуальной сети имеет встроенные системные таблицы маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="46eac-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="46eac-118">Таблица маршрутизации Hello система имеет следующие три группы маршрутов hello:</span><span class="sxs-lookup"><span data-stu-id="46eac-118">hello system routing table has hello following three groups of routes:</span></span>

  * <span data-ttu-id="46eac-119">**Локальные маршруты виртуальной сети:** непосредственно toohello целевым ВМ в hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="46eac-119">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="46eac-120">**Локальные маршруты:** toohello VPN-шлюз Azure.</span><span class="sxs-lookup"><span data-stu-id="46eac-120">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="46eac-121">**Маршрут по умолчанию:** напрямую toohello Интернет.</span><span class="sxs-lookup"><span data-stu-id="46eac-121">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="46eac-122">Пакеты, предназначенные toohello частных IP-адресов не соответствует ни hello предыдущие два маршруты, будут удалены.</span><span class="sxs-lookup"><span data-stu-id="46eac-122">Packets destined toohello private IP addresses not covered by hello previous two routes will be dropped.</span></span>
* <span data-ttu-id="46eac-123">С выпуском hello определяемых пользователем маршрутов можно создать маршрутизации tooadd таблицы маршрут по умолчанию и затем связать hello маршрутизации таблицы tooyour виртуальной сети подсетями tooenable принудительного туннелирования в этих подсетях.</span><span class="sxs-lookup"><span data-stu-id="46eac-123">With hello release of user-defined routes, you can create a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="46eac-124">Необходимо tooset «сайт по умолчанию» среди hello между организациями подключенных toohello локальных сайтов виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="46eac-124">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span>
* <span data-ttu-id="46eac-125">Принудительное туннелирование должно быть сопоставлено с виртуальной сетью, в которой есть VPN-шлюз с динамической маршрутизацией (а не статический шлюз).</span><span class="sxs-lookup"><span data-stu-id="46eac-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="46eac-126">Принудительное туннелирование ExpressRoute не настраивается с помощью этого механизма, но вместо этого обеспечивается объявление маршрута по умолчанию через hello ExpressRoute BGP сеансы пиринга.</span><span class="sxs-lookup"><span data-stu-id="46eac-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="46eac-127">См. в разделе hello [документации по ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="46eac-127">Please see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="46eac-128">Общие сведения о настройке</span><span class="sxs-lookup"><span data-stu-id="46eac-128">Configuration overview</span></span>
<span data-ttu-id="46eac-129">В следующем примере hello проводном hello интерфейсной подсети не является принудительным.</span><span class="sxs-lookup"><span data-stu-id="46eac-129">In hello following example, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="46eac-130">Hello рабочих нагрузок в hello внешней подсети можно продолжить tooaccept и из Интернета hello отвечающего toocustomer запросов.</span><span class="sxs-lookup"><span data-stu-id="46eac-130">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="46eac-131">Hello промежуточной и внутренней подсетях выполняется Принудительное туннелирование.</span><span class="sxs-lookup"><span data-stu-id="46eac-131">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="46eac-132">Все исходящие подключения из этих двух подсетей toohello Интернет будет tooan принудительной или перенаправления обратно на локальный сайт через одну приветствия туннели S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="46eac-132">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="46eac-133">Это позволяет вам toorestrict и инспектировать доступ к Интернету из виртуальных машин или облачных служб в Azure, продолжая tooenable необходимые службы многоуровневые архитектуры.</span><span class="sxs-lookup"><span data-stu-id="46eac-133">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="46eac-134">Также можно применить принудительного туннелирования toohello все виртуальные сети, если отсутствуют рабочие нагрузки с выходом в Интернет в виртуальных сетях.</span><span class="sxs-lookup"><span data-stu-id="46eac-134">You also can apply forced tunneling toohello entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Принудительное туннелирование](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="46eac-136">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="46eac-136">Before you begin</span></span>
<span data-ttu-id="46eac-137">Проверьте наличие следующих элементов перед началом процедуры настройки hello.</span><span class="sxs-lookup"><span data-stu-id="46eac-137">Verify that you have hello following items before beginning configuration.</span></span>

* <span data-ttu-id="46eac-138">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="46eac-138">An Azure subscription.</span></span> <span data-ttu-id="46eac-139">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46eac-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="46eac-140">Настроенная виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="46eac-140">A configured virtual network.</span></span> 
* <span data-ttu-id="46eac-141">Hello последняя версия командлетов Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="46eac-141">hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="46eac-142">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="46eac-142">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="46eac-143">Настройка принудительного туннелирования</span><span class="sxs-lookup"><span data-stu-id="46eac-143">Configure forced tunneling</span></span>
<span data-ttu-id="46eac-144">Привет, после процедуры помогут задать Принудительное туннелирование для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="46eac-144">hello following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="46eac-145">действия по настройке Hello соответствуют файла конфигурации сети toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="46eac-145">hello configuration steps correspond toohello VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="46eac-146">В этом примере hello виртуальной сети «MultiTier-VNet» имеет три подсети: 'Переднего плана» и «Midtier», «Внутренний» подсетей с подключениями четыре перекрестные: «DefaultSiteHQ» и тремя ветвями.</span><span class="sxs-lookup"><span data-stu-id="46eac-146">In this example, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="46eac-147">Hello действия будут hello «DefaultSiteHQ» hello соединение сайта по умолчанию для принудительного туннелирования и настройте hello Midtier и Backend подсети toouse принудительного туннелирования.</span><span class="sxs-lookup"><span data-stu-id="46eac-147">hello steps will set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello Midtier and Backend subnets toouse forced tunneling.</span></span>

1. <span data-ttu-id="46eac-148">Создайте таблицу маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="46eac-148">Create a routing table.</span></span> <span data-ttu-id="46eac-149">Используйте следующий командлет toocreate hello таблицы маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="46eac-149">Use hello following cmdlet toocreate your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="46eac-150">Добавьте таблицу маршрутизации toohello маршрута по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="46eac-150">Add a default route toohello routing table.</span></span> 

  <span data-ttu-id="46eac-151">Hello следующий пример добавляет по умолчанию маршрута toohello таблицу маршрутизации, созданную на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="46eac-151">hello following example adds a default route toohello routing table created in Step 1.</span></span> <span data-ttu-id="46eac-152">Обратите внимание, что hello только поддерживаемый маршрут — hello префикс назначения «0.0.0.0/0» toohello следующего прыжка «VPNGateway».</span><span class="sxs-lookup"><span data-stu-id="46eac-152">Note that hello only route supported is hello destination prefix of "0.0.0.0/0" toohello "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="46eac-153">Свяжите hello маршрутизации таблицы toohello подсети.</span><span class="sxs-lookup"><span data-stu-id="46eac-153">Associate hello routing table toohello subnets.</span></span> 

  <span data-ttu-id="46eac-154">После создания таблицы маршрутизации и добавления маршрута, используйте следующий пример tooadd hello или свяжите маршрута таблицы hello tooa-подсеть виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="46eac-154">After a routing table is created and a route added, use hello following example tooadd or associate hello route table tooa VNet subnet.</span></span> <span data-ttu-id="46eac-155">пример Hello добавляет hello маршрута таблицу «MyRouteTable» toohello Midtier и серверной подсети виртуальной сети MultiTier-VNet.</span><span class="sxs-lookup"><span data-stu-id="46eac-155">hello example adds hello route table "MyRouteTable" toohello Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="46eac-156">Назначьте сайт по умолчанию для принудительного туннелирования.</span><span class="sxs-lookup"><span data-stu-id="46eac-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="46eac-157">В предыдущих шага hello hello демонстрационных скриптах командлетов hello таблицы маршрутизации, которая связывается tootwo таблицы маршрутов hello hello подсетей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="46eac-157">In hello preceding step, hello sample cmdlet scripts created hello routing table and associated hello route table tootwo of hello VNet subnets.</span></span> <span data-ttu-id="46eac-158">Hello осталось tooselect среди межсайтовых подключений hello hello виртуальной сети, что узел по умолчанию hello или туннель.</span><span class="sxs-lookup"><span data-stu-id="46eac-158">hello remaining step is tooselect a local site among hello multi-site connections of hello virtual network as hello default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="46eac-159">Дополнительные командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="46eac-159">Additional PowerShell cmdlets</span></span>
### <a name="toodelete-a-route-table"></a><span data-ttu-id="46eac-160">toodelete таблицы маршрутов</span><span class="sxs-lookup"><span data-stu-id="46eac-160">toodelete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a><span data-ttu-id="46eac-161">toolist таблицы маршрутов</span><span class="sxs-lookup"><span data-stu-id="46eac-161">toolist a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a><span data-ttu-id="46eac-162">toodelete маршрута из таблицы маршрутизации</span><span class="sxs-lookup"><span data-stu-id="46eac-162">toodelete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a><span data-ttu-id="46eac-163">tooremove маршрута из подсети</span><span class="sxs-lookup"><span data-stu-id="46eac-163">tooremove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a><span data-ttu-id="46eac-164">таблицы маршрутов hello toolist, связанной с подсетью</span><span class="sxs-lookup"><span data-stu-id="46eac-164">toolist hello route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="46eac-165">tooremove сайт по умолчанию из шлюза виртуальной сети VPN</span><span class="sxs-lookup"><span data-stu-id="46eac-165">tooremove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```