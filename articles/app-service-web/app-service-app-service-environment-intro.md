---
title: "aaaIntroduction tooApp среды службы v1"
description: "Дополнительные сведения о функции hello v1 среды службы приложений, которая предоставляет единицы масштабирования безопасную, присоединенных к виртуальной сети, выделенных для выполнения всех приложений."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a><span data-ttu-id="c0a28-103">Введение tooApp среды службы v1</span><span class="sxs-lookup"><span data-stu-id="c0a28-103">Introduction tooApp Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="c0a28-104">Эта статья является о hello v1 среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c0a28-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="c0a28-105">Имеется более новая версия hello среды службы приложений, удобнее toouse и выполняется на более мощный инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="c0a28-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="c0a28-106">Дополнительные сведения о новой версии hello начинаться с hello toolearn [toohello введение среды службы приложений](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="c0a28-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="c0a28-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="c0a28-107">Overview</span></span>
<span data-ttu-id="c0a28-108">Среда службы приложений — это план обслуживания [Премиум][PremiumTier] в службе приложений Azure. Она обеспечивает полностью изолированную и выделенную среду для безопасного выполнения приложений службы приложений Azure в большом масштабе, включая [веб-приложения][WebApps], [мобильные приложения][MobileApps] и [приложения API][APIApps].</span><span class="sxs-lookup"><span data-stu-id="c0a28-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="c0a28-109">Среда службы приложений идеально подходит для рабочих нагрузок приложений, требующих выполнения указанных ниже условий.</span><span class="sxs-lookup"><span data-stu-id="c0a28-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="c0a28-110">Очень большой масштаб</span><span class="sxs-lookup"><span data-stu-id="c0a28-110">Very high scale</span></span>
* <span data-ttu-id="c0a28-111">Изоляция и безопасный доступ к сети</span><span class="sxs-lookup"><span data-stu-id="c0a28-111">Isolation and secure network access</span></span>

<span data-ttu-id="c0a28-112">Клиенты могут создавать несколько сред службы приложений как в одном, так и в нескольких регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="c0a28-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="c0a28-113">Благодаря этому среды службы приложений идеально подходят для горизонтально масштабируемых уровней приложений без учета состояний, поддерживающих большие рабочие нагрузки RPS.</span><span class="sxs-lookup"><span data-stu-id="c0a28-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="c0a28-114">Среды службы приложений — это изолированное toorunning только одного клиента приложения и всегда развертываются в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c0a28-114">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="c0a28-115">Клиенты имеют возможность точного управления оба приложения входящий и исходящий сетевой трафик и приложений может устанавливать высокоскоростной безопасные соединения по корпоративным ресурсам локальной tooon виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="c0a28-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="c0a28-116">Все статьи и как-для пользователя о среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="c0a28-116">All articles and How-To's about App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="c0a28-117">Обзор того, как включить высокий уровень масштабирования среды службы приложения и защиты доступа к сети см. в разделе hello [глубокое погружение AzureCon] [ AzureConDeepDive] на среды службы приложений!</span><span class="sxs-lookup"><span data-stu-id="c0a28-117">For an overview of how App Service Environments enable high scale and secure network access, see hello [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="c0a28-118">Глубокое погружение в горизонтальное масштабирование с использованием нескольких средах службы приложения в статье hello о том, как toosetup [объем географически распределенных приложений][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="c0a28-118">For a deep-dive on horizontally scaling using multiple App Service Environments see hello article on how toosetup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="c0a28-119">toosee, как показано в hello AzureCon подробная архитектура безопасности hello был настроен, см. в статье hello в первую очередь реализация [многоуровневая архитектура безопасности](app-service-app-service-environment-layered-security.md) с среды службы приложения.</span><span class="sxs-lookup"><span data-stu-id="c0a28-119">toosee how hello security architecture shown in hello AzureCon Deep Dive was configured, see hello article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="c0a28-120">Приложения, работающие в средах службы приложений, могут получать доступ через такие устройства, как брандмауэр веб-приложений (WAF).</span><span class="sxs-lookup"><span data-stu-id="c0a28-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="c0a28-121">Hello статьи на [Настройка WAF для среды службы приложения](app-service-app-service-environment-web-application-firewall.md) рассматриваются в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="c0a28-121">hello article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="c0a28-122">Выделенные вычислительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c0a28-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="c0a28-123">Все hello вычислительных ресурсов в среде службы приложений выделенных исключительно tooa одной подписке, и среды службы приложений можно настроить с помощью копирования (50) toofifty вычислительные ресурсы для монопольного использования одним приложением.</span><span class="sxs-lookup"><span data-stu-id="c0a28-123">All of hello compute resources in an App Service Environment are dedicated exclusively tooa single subscription, and an App Service Environment can be configured with up toofifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="c0a28-124">Среды службы приложений состоит из пула ресурсов вычислений переднего плана, а также вычислительных ресурсов один toothree рабочих пулов.</span><span class="sxs-lookup"><span data-stu-id="c0a28-124">An App Service Environment is composed of a front-end compute resource pool, as well as one toothree worker compute resource pools.</span></span> 

<span data-ttu-id="c0a28-125">внешний пул Hello содержит вычислительные ресурсы, ответственные за завершение запросов SSL как Балансировка нагрузки также автоматического запросов приложения в среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c0a28-125">hello front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="c0a28-126">Каждый пул рабочих содержит вычислительные ресурсы, выделенные слишком[планы службы приложений][AppServicePlan], который в свою очередь содержать одно или несколько приложений службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="c0a28-126">Each worker pool contains compute resources allocated too[App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="c0a28-127">Поскольку может существовать вверх toothree различных рабочих пулов в среде службы приложений, у вас есть hello гибкость toochoose различных вычислительных ресурсов для каждого рабочего пула.</span><span class="sxs-lookup"><span data-stu-id="c0a28-127">Since there can be up toothree different worker pools in an App Service Environment, you have hello flexibility toochoose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="c0a28-128">Например это позволяет toocreate пул один рабочий процесс с менее мощных вычислительных ресурсов для приложения службы планы предназначен для разработки и тестирования приложений.</span><span class="sxs-lookup"><span data-stu-id="c0a28-128">For example, this allows you toocreate one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="c0a28-129">Второй (или даже третий) рабочий пул может использовать более мощные вычислительные ресурсы, предназначенные для планов службы приложений с запущенными производственными приложениями.</span><span class="sxs-lookup"><span data-stu-id="c0a28-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="c0a28-130">Дополнительные сведения о hello количество вычислительных ресурсов доступны toohello переднего плана и рабочих пулов см. в разделе [как tooConfigure среды службы приложений][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="c0a28-130">For more details on hello quantity of compute resources available toohello front-end and worker pools, see [How tooConfigure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="c0a28-131">Для сведения о доступных hello вычислений ресурсов размеры, поддерживаемые в среде службы приложений, обратитесь к hello [цены на службу приложения] [ AppServicePricing] страницы и просмотрите доступные параметры среды службы приложения hello в ценовой категории "премиум" hello.</span><span class="sxs-lookup"><span data-stu-id="c0a28-131">For details on hello available compute resource sizes supported in an App Service Environment, consult hello [App Service Pricing][AppServicePricing] page and review hello available options for App Service Environments in hello Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="c0a28-132">Поддержка виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="c0a28-132">Virtual Network Support</span></span>
<span data-ttu-id="c0a28-133">Среду службы приложений можно создать **либо** в виртуальной сети Azure Resource Manager, **либо** в виртуальной сети, использующей классическую модель развертывания. Вы можете [узнать больше о виртуальных сетях][MoreInfoOnVirtualNetworks].</span><span class="sxs-lookup"><span data-stu-id="c0a28-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="c0a28-134">Поскольку всегда существует среды службы приложений в виртуальной сети и точнее в подсети виртуальной сети, можно использовать оба входящего и исходящего сетевого взаимодействия технологии безопасности hello toocontrol виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="c0a28-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage hello security features of virtual networks toocontrol both inbound and outbound network communications.</span></span>  

<span data-ttu-id="c0a28-135">Среда службы приложений может быть доступной из Интернета с использованием общедоступного IP-адреса или из внутренней системы с использованием адреса внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="c0a28-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="c0a28-136">Можно использовать [сетевых групп безопасности] [ NetworkSecurityGroups] toorestrict входящие связи toohello подсети, к которой находится среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c0a28-136">You can use [network security groups][NetworkSecurityGroups] toorestrict inbound network communications toohello subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="c0a28-137">Это позволяет toorun приложения за вышестоящего устройств и служб, таких как брандмауэры приложения web и поставщики SaaS сети.</span><span class="sxs-lookup"><span data-stu-id="c0a28-137">This allows you toorun apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="c0a28-138">Приложения, должны также часто tooaccess корпоративным ресурсам, например внутренними базами данных и веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c0a28-138">Apps also frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="c0a28-139">Наиболее распространенный подход является toomake эти конечные точки доступны только toointernal сетевой трафик в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="c0a28-139">A common approach is toomake these endpoints available only toointernal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="c0a28-140">После среды службы приложений присоединены к домену toohello одной виртуальной сети как hello внутренней службы, приложения, выполняющиеся в среде hello могли обращаться к ним, включая конечные точки с помощью [сайт-сайт] [ SiteToSite]и [Azure ExpressRoute] [ ExpressRoute] подключений.</span><span class="sxs-lookup"><span data-stu-id="c0a28-140">Once an App Service Environment is joined toohello same virtual network as hello internal services, apps running in hello environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="c0a28-141">Дополнительную информацию о работе с виртуальными сетями и локальными сетями среды службы приложений можно найти следующие статьи hello [архитектура сети][NetworkArchitectureOverview], [управление входящих подключений Трафик][ControllingInboundTraffic], и [безопасного соединения tooBackends][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="c0a28-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult hello following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting tooBackends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="c0a28-142">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="c0a28-142">Getting started</span></span>
<span data-ttu-id="c0a28-143">tooget к работе с среды службы приложения, в разделе [как tooCreate среды службы приложений][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="c0a28-143">tooget started with App Service Environments, see [How tooCreate An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="c0a28-144">Все статьи и как-для пользователя для среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="c0a28-144">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="c0a28-145">Дополнительные сведения о платформе hello службе приложений Azure см. в разделе [службе приложений Azure][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="c0a28-145">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="c0a28-146">Обзор hello архитектура сети среды службы приложений см. в разделе hello [Обзор архитектуры сети] [ NetworkArchitectureOverview] статьи.</span><span class="sxs-lookup"><span data-stu-id="c0a28-146">For an overview of hello App Service Environment network architecture, see hello [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="c0a28-147">Сведения об использовании среды службы приложений при помощи ExpressRoute см. в следующей статьей hello [Express Route и среды службы приложения][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="c0a28-147">For details on using an App Service Environment with ExpressRoute, see hello following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


