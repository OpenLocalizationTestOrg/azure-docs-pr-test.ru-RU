---
title: "Безопасное подключение к серверным ресурсам из среды службы приложений"
description: "Подробные сведения о безопасном подключении к серверным ресурсам из среды службы приложений."
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
ms.openlocfilehash: 0b6d3a47dc429c469b37c2c74f546cfeca580358
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="d836a-103">Безопасное подключение к серверным ресурсам из среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="d836a-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="d836a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d836a-104">Overview</span></span>
<span data-ttu-id="d836a-105">Так как среда службы приложений всегда создается **либо** в виртуальной сети Azure Resource Manager, **либо** в [виртуальной сети][virtualnetwork], использующей классическую модель развертывания, исходящие подключения из среды службы приложений к другим внутренним ресурсам могут передаваться исключительно по виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d836a-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="d836a-106">В связи с последним изменением от июня 2016 г. среды ASE можно также развертывать в виртуальных сетях, использующих либо диапазоны общедоступных адресов, либо адресные пространства RFC1918 (т. е.</span><span class="sxs-lookup"><span data-stu-id="d836a-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="d836a-107">частные адреса).</span><span class="sxs-lookup"><span data-stu-id="d836a-107">private addresses).</span></span>  

<span data-ttu-id="d836a-108">Например, SQL Server может работать в кластере виртуальных машин с заблокированным портом 1433.</span><span class="sxs-lookup"><span data-stu-id="d836a-108">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="d836a-109">Конечная точка может быть ACLd, разрешая только доступ от других ресурсов в той же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d836a-109">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="d836a-110">Другой пример: конфиденциальные конечные точки могут выполняться локально и быть подключены к Azure через подключение типа [сеть — сеть][SiteToSite] или канал [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="d836a-110">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="d836a-111">В результате только ресурсы в виртуальной сети, подключенной к туннелям "сеть-сеть" или ExpressRoute, смогут иметь доступ к локальным конечным точкам.</span><span class="sxs-lookup"><span data-stu-id="d836a-111">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="d836a-112">Во всех этих сценариях приложения, выполняемые в среде службы приложений, смогут безопасно подключаться к различным серверам и ресурсам.</span><span class="sxs-lookup"><span data-stu-id="d836a-112">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="d836a-113">Исходящий трафик от приложений, выполняемых в среде службы приложений, к частным конечным точкам в той же виртуальной сети (или подключенным к той же виртуальной сети), будет идти только по виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d836a-113">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="d836a-114">Исходящий трафик к частным конечным точкам не будет проходить через общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="d836a-114">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="d836a-115">Одно из предупреждений применяется для исходящего трафика из среды службы приложений к конечным точкам в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d836a-115">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="d836a-116">Среды службы приложений не могут достичь конечных точек виртуальных машин, расположенных в **той же** подсети, что и среда службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d836a-116">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="d836a-117">Обычно это не должно быть проблемой при условии, что среды службы приложений развертываются в подсеть, зарезервированную для монопольного использования средой службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d836a-117">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="d836a-118">Требования к DNS и исходящим подключениям</span><span class="sxs-lookup"><span data-stu-id="d836a-118">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="d836a-119">Для надлежащего функционирования среды службы приложений требуется исходящий доступ к различным конечным точкам.</span><span class="sxs-lookup"><span data-stu-id="d836a-119">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="d836a-120">Полный список внешних конечных точек, используемых в ASE, приведен в разделе "Необходимое сетевое подключение" статьи [Сведения о конфигурации сети для сред службы приложений с ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) .</span><span class="sxs-lookup"><span data-stu-id="d836a-120">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="d836a-121">Для сред службы приложений требуется, чтобы для виртуальной сети была настроена допустимая инфраструктура DNS.</span><span class="sxs-lookup"><span data-stu-id="d836a-121">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="d836a-122">Если после создания среды службы приложений по какой-либо причине меняется конфигурация DNS, разработчик может принудительно задать выбор новой конфигурации DNS в среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d836a-122">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="d836a-123">Перезагрузка разворачиваемой среды с помощью значка "Перезапуск", расположенного в верхней части колонки управления средой службы приложений на портале, приведет к выбору новой конфигурации DNS в среде.</span><span class="sxs-lookup"><span data-stu-id="d836a-123">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="d836a-124">Также рекомендуется настроить пользовательские DNS-серверы в виртуальной сети заранее, т. е. до создания среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d836a-124">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="d836a-125">Если конфигурация виртуальной сети DNS изменяется во время создания среды службы приложений, это приведет к сбою процесса создания среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d836a-125">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="d836a-126">Аналогично, если на другой стороне VPN-шлюза имеется пользовательский DNS-сервер, который недоступен, процесс создания среды службы приложений будет прерван.</span><span class="sxs-lookup"><span data-stu-id="d836a-126">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="d836a-127">Подключение к SQL Server</span><span class="sxs-lookup"><span data-stu-id="d836a-127">Connecting to a SQL Server</span></span>
<span data-ttu-id="d836a-128">В типичной конфигурации SQL Server конечная точка прослушивает порт 1433:</span><span class="sxs-lookup"><span data-stu-id="d836a-128">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Конечная точка сервера SQL Server][SqlServerEndpoint]

<span data-ttu-id="d836a-130">Существует два подхода к ограничению трафика к этой конечной точке.</span><span class="sxs-lookup"><span data-stu-id="d836a-130">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="d836a-131">[Сетевые списки управления доступом][NetworkAccessControlLists] (сетевые ACL).</span><span class="sxs-lookup"><span data-stu-id="d836a-131">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="d836a-132">[Группы безопасности сети][NetworkSecurityGroups].</span><span class="sxs-lookup"><span data-stu-id="d836a-132">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="d836a-133">Ограничение доступа с помощью сетевых списков управления доступом</span><span class="sxs-lookup"><span data-stu-id="d836a-133">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="d836a-134">Порт 1433 можно защитить с помощью сетевого списка управления доступом.</span><span class="sxs-lookup"><span data-stu-id="d836a-134">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="d836a-135">В примере ниже адреса клиентов из виртуальной сети добавляются в белый список, а доступ ко всем других клиентам блокируется.</span><span class="sxs-lookup"><span data-stu-id="d836a-135">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![Пример сетевого списка управления доступом][NetworkAccessControlListExample]

<span data-ttu-id="d836a-137">Все приложения, работающего в среде службы приложений в той же виртуальной сети, что и SQL Server, смогут подключиться к экземпляру SQL Server с помощью внутреннего IP-адреса **виртуальной сети** для виртуальной машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d836a-137">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="d836a-138">Пример строки подключения ниже ссылается на SQL Server, использующий частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="d836a-138">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="d836a-139">Хотя виртуальная машина имеет также общедоступную конечную точку, попытки подключения с использованием общедоступного IP-адреса будут отклонены из-за использования сетевых списков управления доступом.</span><span class="sxs-lookup"><span data-stu-id="d836a-139">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="d836a-140">Ограничение доступа с помощью группы сетевой безопасности</span><span class="sxs-lookup"><span data-stu-id="d836a-140">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="d836a-141">Альтернативный подход для обеспечения безопасного доступа заключается в использовании группы сетевой безопасности.</span><span class="sxs-lookup"><span data-stu-id="d836a-141">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="d836a-142">Группы сетевой безопасности можно применять к отдельным виртуальным машинам или к подсети, содержащей виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="d836a-142">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="d836a-143">Сначала необходимо создать группу сетевой безопасности:</span><span class="sxs-lookup"><span data-stu-id="d836a-143">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="d836a-144">Ограничить доступ только для внутреннего трафика виртуальной сети очень просто с помощью группы сетевой безопасности.</span><span class="sxs-lookup"><span data-stu-id="d836a-144">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="d836a-145">Правила по умолчанию в группе сетевой безопасности разрешают доступ только от других сетевых клиентов в той же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d836a-145">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="d836a-146">В результате, блокирование доступа к SQL Server сводится к применению группы сетевой безопасности с ее правилами по умолчанию либо к работающим виртуальным машинам, где запущен SQL Server, либо к подсети, содержащей виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="d836a-146">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="d836a-147">В следующем примере группа сетевой безопасности применяется к содержащей подсети:</span><span class="sxs-lookup"><span data-stu-id="d836a-147">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="d836a-148">Конечным результатом является набор правил безопасности, которые блокируют внешний доступ, предоставляя внутренний доступ из виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="d836a-148">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Правила сетевой безопасности по умолчанию][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="d836a-150">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="d836a-150">Getting started</span></span>
<span data-ttu-id="d836a-151">Все статьи и практические руководства, посвященные средам службы приложений, доступны в [файле сведений для сред службы приложений](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="d836a-151">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="d836a-152">Сведения о том, как начать работу со средами службы приложений, см. в статье [Введение в среду службы приложений][IntroToAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="d836a-152">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="d836a-153">Дополнительные сведения об управлении входящим трафиком в среде службы приложений см. в разделе [Как управлять входящим трафиком в среде службы приложений][ControlInboundASE].</span><span class="sxs-lookup"><span data-stu-id="d836a-153">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="d836a-154">Дополнительные сведения о платформе службы приложений Azure см. в статье [Что такое служба приложений Azure?][AzureAppService]</span><span class="sxs-lookup"><span data-stu-id="d836a-154">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
