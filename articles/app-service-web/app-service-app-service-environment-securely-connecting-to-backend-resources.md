---
title: "Подключение aaaSecurely tooBackEnd ресурсов из среды службы приложений"
description: "Дополнительные сведения о подключении ресурсы toobackend toosecurely из среды службы приложений."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a><span data-ttu-id="93989-103">Безопасное подключение tooBackend ресурсов из среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="93989-103">Securely Connecting tooBackend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="93989-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="93989-104">Overview</span></span>
<span data-ttu-id="93989-105">Поскольку всегда создается в среде службы приложений **либо** виртуальной сетью Azure Resource Manager **или** классической модели развертывания [виртуальной сети] [ virtualnetwork], могут передавать исходящие подключения из среды службы приложений tooother внутренних ресурсов исключительно через hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="93989-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment tooother backend resources can flow exclusively over hello virtual network.</span></span>  <span data-ttu-id="93989-106">В связи с последним изменением от июня 2016 г. среды ASE можно также развертывать в виртуальных сетях, использующих либо диапазоны общедоступных адресов, либо адресные пространства RFC1918 (т. е. частные адреса).</span><span class="sxs-lookup"><span data-stu-id="93989-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="93989-107">Например, SQL Server может работать в кластере виртуальных машин с заблокированным портом 1433.</span><span class="sxs-lookup"><span data-stu-id="93989-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="93989-108">Hello конечная точка может быть ACLd tooonly разрешения доступа от других ресурсов на hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="93989-108">hello endpoint may be ACLd tooonly allow access from other resources on hello same virtual network.</span></span>  

<span data-ttu-id="93989-109">Еще один пример, конфиденциальные конечные точки могут и локально и быть подключенным tooAzure через либо [сайт-сайт] [ SiteToSite] или [Azure ExpressRoute] [ ExpressRoute] подключений.</span><span class="sxs-lookup"><span data-stu-id="93989-109">As another example, sensitive endpoints may run on-premises and be connected tooAzure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="93989-110">В результате только ресурсов в виртуальные сети подключены toohello сайт-сайт или ExpressRoute туннели будут конечными точками в локальной среде может tooaccess.</span><span class="sxs-lookup"><span data-stu-id="93989-110">As a result, only resources in virtual networks connected toohello Site-to-Site or ExpressRoute tunnels will be able tooaccess on-premises endpoints.</span></span>

<span data-ttu-id="93989-111">Для всех этих сценариях приложений, выполняемых в среде службы приложений будет может toosecurely подключения toohello различные серверы и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="93989-111">For all of these scenarios, apps running on an App Service Environment will be able toosecurely connect toohello various servers and resources.</span></span>  <span data-ttu-id="93989-112">Исходящий трафик из приложения, выполняющиеся в среде службы приложений tooprivate конечных точек в hello одной виртуальной сети (или подключенных toohello одной виртуальной сети), будут только поток hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="93989-112">Outbound traffic from apps running in an App Service Environment tooprivate endpoints in hello same virtual network (or connected toohello same virtual network), will only flow over hello virtual network.</span></span>  <span data-ttu-id="93989-113">Исходящий трафик tooprivate, конечные точки не будет передаваться через hello общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="93989-113">Outbound traffic tooprivate endpoints will not flow over hello public Internet.</span></span>

<span data-ttu-id="93989-114">Один нюанс применяется toooutbound трафика от tooendpoints среды службы приложений в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="93989-114">One caveat applies toooutbound traffic from an App Service Environment tooendpoints within a virtual network.</span></span>  <span data-ttu-id="93989-115">Среды службы приложения не могут достичь конечных точек виртуальных машин, размещенных в hello **же** подсети как hello среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="93989-115">App Service Environments cannot reach endpoints of virtual machines located in hello **same** subnet as hello App Service Environment.</span></span>  <span data-ttu-id="93989-116">Это обычно не должна быть проблемой при условии, что среды службы приложений, развернутых в подсети, зарезервированные для монопольного использования только hello среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="93989-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only hello App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="93989-117">Требования к DNS и исходящим подключениям</span><span class="sxs-lookup"><span data-stu-id="93989-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="93989-118">Надлежащим образом, для среды службы приложений toofunction требуются конечные точки toovarious исходящий доступ.</span><span class="sxs-lookup"><span data-stu-id="93989-118">For an App Service Environment toofunction properly, it requires outbound access toovarious endpoints.</span></span> <span data-ttu-id="93989-119">Полный список hello внешних конечных точек, используемых ASE представлен в hello раздел «Требуется сетевое подключение» hello [конфигурацию сети для ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) статьи.</span><span class="sxs-lookup"><span data-stu-id="93989-119">A full list of hello external endpoints used by an ASE is in hello "Required Network Connectivity" section of hello [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="93989-120">Среды службы приложений требуется допустимый инфраструктура DNS настроен для hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="93989-120">App Service Environments require a valid DNS infrastructure configured for hello virtual network.</span></span>  <span data-ttu-id="93989-121">Если для любого hello причина будет изменена конфигурация DNS после создания среды службы приложений, разработчики можно принудительно toopick среды службы приложения hello новой конфигурации DNS.</span><span class="sxs-lookup"><span data-stu-id="93989-121">If for any reason hello DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment toopick up hello new DNS configuration.</span></span>  <span data-ttu-id="93989-122">Последовательное среды перезагрузку, используя значок «Перезапуск» hello, расположенный вверху hello hello среды службы приложений колонке управления hello портала приведет к toopick среды hello hello новой конфигурации DNS.</span><span class="sxs-lookup"><span data-stu-id="93989-122">Triggering a rolling environment reboot using hello "Restart" icon located at hello top of hello App Service Environment management blade in hello portal will cause hello environment toopick up hello new DNS configuration.</span></span>

<span data-ttu-id="93989-123">Также рекомендуется обеспечить пользовательские DNS-серверы в виртуальной сети hello установки опережает время предыдущего toocreating среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="93989-123">It is also recommended that any custom DNS servers on hello vnet be setup ahead of time prior toocreating an App Service Environment.</span></span>  <span data-ttu-id="93989-124">При создании среды службы приложений при изменении конфигурации DNS виртуальной сети, приведет к сбой процесса создания среды службы приложений hello.</span><span class="sxs-lookup"><span data-stu-id="93989-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in hello App Service Environment creation process failing.</span></span>  <span data-ttu-id="93989-125">Если существует пользовательского DNS-сервера на приветствия другом конце VPN-шлюза и DNS-сервер hello в аналогичные вена, является hello недоступен или недоступен, произойдет сбой процесса создания среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="93989-125">In a similar vein, if a custom DNS server exists on hello other end of a VPN gateway, and hello DNS server is unreachable or unavailable, hello App Service Environment creation process will also fail.</span></span>

## <a name="connecting-tooa-sql-server"></a><span data-ttu-id="93989-126">Подключение tooa SQL Server</span><span class="sxs-lookup"><span data-stu-id="93989-126">Connecting tooa SQL Server</span></span>
<span data-ttu-id="93989-127">В типичной конфигурации SQL Server конечная точка прослушивает порт 1433:</span><span class="sxs-lookup"><span data-stu-id="93989-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Конечная точка сервера SQL Server][SqlServerEndpoint]

<span data-ttu-id="93989-129">Существует два подхода для ограничения трафика toothis endpoint:</span><span class="sxs-lookup"><span data-stu-id="93989-129">There are two approaches for restricting traffic toothis endpoint:</span></span>

* <span data-ttu-id="93989-130">[Сетевые списки управления доступом][NetworkAccessControlLists] (сетевые ACL).</span><span class="sxs-lookup"><span data-stu-id="93989-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="93989-131">[Группы безопасности сети][NetworkSecurityGroups].</span><span class="sxs-lookup"><span data-stu-id="93989-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="93989-132">Ограничение доступа с помощью сетевых списков управления доступом</span><span class="sxs-lookup"><span data-stu-id="93989-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="93989-133">Порт 1433 можно защитить с помощью сетевого списка управления доступом.</span><span class="sxs-lookup"><span data-stu-id="93989-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="93989-134">пример Hello ниже запрещенного клиента адреса, исходящих от внутри виртуальной сети и блокирует доступ tooall других клиентов.</span><span class="sxs-lookup"><span data-stu-id="93989-134">hello example below whitelists client addresses originating from inside of a virtual network, and blocks access tooall other clients.</span></span>

![Пример сетевого списка управления доступом][NetworkAccessControlListExample]

<span data-ttu-id="93989-136">Hello всем приложениям, выполняющимся в среде службы приложений в одной виртуальной сети, как hello SQL Server будет может tooconnect toohello экземпляром SQL Server hello **внутренней виртуальной сети** IP-адрес для виртуальной машины SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="93989-136">Any applications running in App Service Environment in hello same virtual network as hello SQL Server will be able tooconnect toohello SQL Server instance using hello **VNet internal** IP address for hello SQL Server virtual machine.</span></span>  

<span data-ttu-id="93989-137">Пример строки подключения Hello ниже ссылки hello SQL Server, используя свой закрытый IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="93989-137">hello example connection string below references hello SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="93989-138">Несмотря на то, что виртуальная машина hello содержит также общедоступную конечную точку, попытки подключения с помощью hello общедоступный IP-адрес, будут отклонены из-за hello управления сетевым Доступом.</span><span class="sxs-lookup"><span data-stu-id="93989-138">Although hello virtual machine has a public endpoint as well, connection attempts using hello public IP address will be rejected because of hello network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="93989-139">Ограничение доступа с помощью группы сетевой безопасности</span><span class="sxs-lookup"><span data-stu-id="93989-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="93989-140">Альтернативный подход для обеспечения безопасного доступа заключается в использовании группы сетевой безопасности.</span><span class="sxs-lookup"><span data-stu-id="93989-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="93989-141">Сетевые группы безопасности может быть применен tooindividual виртуальных машин или tooa подсети, содержащие виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="93989-141">Network security groups can be applied tooindividual virtual machines, or tooa subnet containing virtual machines.</span></span>

<span data-ttu-id="93989-142">Сначала сетевую группу безопасности требуется toobe создан:</span><span class="sxs-lookup"><span data-stu-id="93989-142">First a network security group needs toobe created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="93989-143">Ограничение доступа tooonly внутренний трафик виртуальной сети является очень простым с сетевой группой безопасности.</span><span class="sxs-lookup"><span data-stu-id="93989-143">Restricting access tooonly VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="93989-144">правила по умолчанию Hello в группу безопасности сети только разрешить доступ из других сетевых клиентов в hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="93989-144">hello default rules in a network security group only allow access from other network clients in hello same virtual network.</span></span>

<span data-ttu-id="93989-145">В результате блокирования доступа tooSQL сервера заключается в применении группы безопасности сети с его по умолчанию правила tooeither hello виртуальные машины под управлением SQL Server или подсети hello, содержащие виртуальные машины hello.</span><span class="sxs-lookup"><span data-stu-id="93989-145">As a result locking down access tooSQL Server is as simple as applying a network security group with its default rules tooeither hello virtual machines running SQL Server, or hello subnet containing hello virtual machines.</span></span>

<span data-ttu-id="93989-146">Образец Hello ниже применяется безопасности группы toohello содержащего подсети:</span><span class="sxs-lookup"><span data-stu-id="93989-146">hello sample below applies a network security group toohello containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="93989-147">Hello конечным результатом является набор правил безопасности, блокирующие внешний доступ, предоставляя внутреннего доступа виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="93989-147">hello end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Правила сетевой безопасности по умолчанию][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="93989-149">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="93989-149">Getting started</span></span>
<span data-ttu-id="93989-150">Все статьи и как-для пользователя для среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="93989-150">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="93989-151">tooget к работе с среды службы приложения, в разделе [tooApp введение среды службы][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="93989-151">tooget started with App Service Environments, see [Introduction tooApp Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="93989-152">Вокруг управляющий входящий трафик tooyour среды службы приложений Подробнее [управление tooan входящего трафика среды службы приложений][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="93989-152">For details around controlling inbound traffic tooyour App Service Environment, see [Controlling inbound traffic tooan App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="93989-153">Дополнительные сведения о платформе hello службе приложений Azure см. в разделе [службе приложений Azure][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="93989-153">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
