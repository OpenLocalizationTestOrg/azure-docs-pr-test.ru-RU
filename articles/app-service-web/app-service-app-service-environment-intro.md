---
title: "Введение в среду службы приложения версии 1"
description: "Сведения о функции среды службы приложений версии 1, которая предоставляет безопасные выделенные единицы масштабирования, присоединенные к виртуальной сети, для выполнения всех ваших приложений."
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
ms.openlocfilehash: 38cb79eb32bd61cdbfb6da91d50e6713d71a2b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-app-service-environment-v1"></a><span data-ttu-id="489e6-103">Введение в среду службы приложения версии 1</span><span class="sxs-lookup"><span data-stu-id="489e6-103">Introduction to App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="489e6-104">Эта статья посвящена среде службы приложений версии 1.</span><span class="sxs-lookup"><span data-stu-id="489e6-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="489e6-105">Имеется более новая версия среды службы приложений, которая проще в использовании и которая работает на более мощной инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="489e6-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="489e6-106">Чтобы узнать больше о новой версии, начните с изучения статьи [Введение в среду службы приложения](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="489e6-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="489e6-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="489e6-107">Overview</span></span>
<span data-ttu-id="489e6-108">Среда службы приложений — это план обслуживания [Премиум][PremiumTier] в службе приложений Azure. Она обеспечивает полностью изолированную и выделенную среду для безопасного выполнения приложений службы приложений Azure в большом масштабе, включая [веб-приложения][WebApps], [мобильные приложения][MobileApps] и [приложения API][APIApps].</span><span class="sxs-lookup"><span data-stu-id="489e6-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="489e6-109">Среда службы приложений идеально подходит для рабочих нагрузок приложений, требующих выполнения указанных ниже условий.</span><span class="sxs-lookup"><span data-stu-id="489e6-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="489e6-110">Очень большой масштаб</span><span class="sxs-lookup"><span data-stu-id="489e6-110">Very high scale</span></span>
* <span data-ttu-id="489e6-111">Изоляция и безопасный доступ к сети</span><span class="sxs-lookup"><span data-stu-id="489e6-111">Isolation and secure network access</span></span>

<span data-ttu-id="489e6-112">Клиенты могут создавать несколько сред службы приложений как в одном, так и в нескольких регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="489e6-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="489e6-113">Благодаря этому среды службы приложений идеально подходят для горизонтально масштабируемых уровней приложений без учета состояний, поддерживающих большие рабочие нагрузки RPS.</span><span class="sxs-lookup"><span data-stu-id="489e6-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="489e6-114">Среды службы приложений изолированы, позволяют запускать приложения только одного клиента и всегда развернуты в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="489e6-114">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="489e6-115">Клиенты могут детально управлять входящим и исходящим сетевым трафиком приложений, а приложения могут создавать высокоскоростные безопасные подключения к локальным корпоративным ресурсам через виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="489e6-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="489e6-116">Все статьи и практические руководства, посвященные средам службы приложений, доступны в [файле сведений для сред службы приложений](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="489e6-116">All articles and How-To's about App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="489e6-117">Общие сведения о том, как среды службы приложений обеспечивают высокую степень масштабирования и безопасный сетевой доступ, доступны в видео [Deploying highly scalable and secure web and mobile apps][AzureConDeepDive] (Развертывание высокомасштабируемых и защищенных веб-приложений и мобильных приложений).</span><span class="sxs-lookup"><span data-stu-id="489e6-117">For an overview of how App Service Environments enable high scale and secure network access, see the [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="489e6-118">Подробный обзор горизонтального масштабирования с помощью нескольких сред службы приложений см. в статье о настройке [географически распределенного приложения][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="489e6-118">For a deep-dive on horizontally scaling using multiple App Service Environments see the article on how to setup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="489e6-119">Чтобы ознакомиться с настройкой архитектуры в подробном обзоре AzureCon, обратитесь к статье о реализации [многоуровневой архитектуры безопасности](app-service-app-service-environment-layered-security.md) со средами службы приложений.</span><span class="sxs-lookup"><span data-stu-id="489e6-119">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="489e6-120">Приложения, работающие в средах службы приложений, могут получать доступ через такие устройства, как брандмауэр веб-приложений (WAF).</span><span class="sxs-lookup"><span data-stu-id="489e6-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="489e6-121">Этот сценарий рассматривается в статье [Настройка WAF для сред службы приложений](app-service-app-service-environment-web-application-firewall.md) .</span><span class="sxs-lookup"><span data-stu-id="489e6-121">The article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="489e6-122">Выделенные вычислительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="489e6-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="489e6-123">Все вычислительные ресурсы в среде службы приложений выделены исключительно для одной подписки. Для среды службы приложений можно настроить до 50 вычислительных ресурсов для монопольного использования одним приложением.</span><span class="sxs-lookup"><span data-stu-id="489e6-123">All of the compute resources in an App Service Environment are dedicated exclusively to a single subscription, and an App Service Environment can be configured with up to fifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="489e6-124">В среду службы приложений входит один интерфейсный пул вычислительных ресурсов, а также от одного до трех рабочих пулов вычислительных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="489e6-124">An App Service Environment is composed of a front-end compute resource pool, as well as one to three worker compute resource pools.</span></span> 

<span data-ttu-id="489e6-125">Интерфейсный пул содержит вычислительные ресурсы, ответственные за завершение SSL-запросов, а также за автоматическую балансировку нагрузки запросов приложений в среде службы приложений.</span><span class="sxs-lookup"><span data-stu-id="489e6-125">The front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="489e6-126">Каждый рабочий пул содержит вычислительные ресурсы, выделенные для [планов службы приложений][AppServicePlan], которые в свою очередь содержат одно или несколько приложений службы приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="489e6-126">Each worker pool contains compute resources allocated to [App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="489e6-127">Поскольку в среде службы приложений может существовать до трех разных рабочих пулов, существует возможность выбирать различные вычислительные ресурсы для каждого рабочего пула.</span><span class="sxs-lookup"><span data-stu-id="489e6-127">Since there can be up to three different worker pools in an App Service Environment, you have the flexibility to choose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="489e6-128">Например, это позволяет создавать один рабочий пул с менее мощными вычислительными ресурсами для планов службы приложений, предназначенных для разработки или тестирования приложений.</span><span class="sxs-lookup"><span data-stu-id="489e6-128">For example, this allows you to create one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="489e6-129">Второй (или даже третий) рабочий пул может использовать более мощные вычислительные ресурсы, предназначенные для планов службы приложений с запущенными производственными приложениями.</span><span class="sxs-lookup"><span data-stu-id="489e6-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="489e6-130">Дополнительные сведения о количестве вычислительных ресурсов, доступных для интерфейсных и рабочих пулов, см. в статье [Настройка среды службы приложений][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="489e6-130">For more details on the quantity of compute resources available to the front-end and worker pools, see [How To Configure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="489e6-131">Дополнительные сведения о доступных размерах вычислительных ресурсов, поддерживаемых в среде службы приложений, см. на странице [Служба приложений: цены][AppServicePricing] в разделе о ценовой категории "Премиум", где можно ознакомиться с доступными вариантами для сред службы приложений.</span><span class="sxs-lookup"><span data-stu-id="489e6-131">For details on the available compute resource sizes supported in an App Service Environment, consult the [App Service Pricing][AppServicePricing] page and review the available options for App Service Environments in the Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="489e6-132">Поддержка виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="489e6-132">Virtual Network Support</span></span>
<span data-ttu-id="489e6-133">Среду службы приложений можно создать **либо** в виртуальной сети Azure Resource Manager, **либо** в виртуальной сети, использующей классическую модель развертывания. Вы можете [узнать больше о виртуальных сетях][MoreInfoOnVirtualNetworks].</span><span class="sxs-lookup"><span data-stu-id="489e6-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="489e6-134">Так как среда службы приложений всегда существует в виртуальной сети, а точнее в подсети виртуальной сети, можно использовать средства безопасности виртуальных сетей для управления как входящими, так и исходящими подключениями в сети.</span><span class="sxs-lookup"><span data-stu-id="489e6-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage the security features of virtual networks to control both inbound and outbound network communications.</span></span>  

<span data-ttu-id="489e6-135">Среда службы приложений может быть доступной из Интернета с использованием общедоступного IP-адреса или из внутренней системы с использованием адреса внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="489e6-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="489e6-136">Можно использовать [группы безопасности сети][NetworkSecurityGroups] для ограничения входящих сетевых подключений для подсети, где находится среда службы приложений.</span><span class="sxs-lookup"><span data-stu-id="489e6-136">You can use [network security groups][NetworkSecurityGroups] to restrict inbound network communications to the subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="489e6-137">Это позволяет запускать приложения за вышестоящими устройствами и службами, например брандмауэрами веб-приложений и поставщиками SaaS сети.</span><span class="sxs-lookup"><span data-stu-id="489e6-137">This allows you to run apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="489e6-138">Приложениям также часто требуется доступ к корпоративным ресурсам, таким как внутренние базы данных и веб-службы.</span><span class="sxs-lookup"><span data-stu-id="489e6-138">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="489e6-139">Наиболее распространенный подход заключается в том, чтобы сделать эти конечные точки доступными только для внутреннего сетевого трафика в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="489e6-139">A common approach is to make these endpoints available only to internal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="489e6-140">После присоединения среды службы приложений к виртуальной сети, в которой размещены внутренние службы, запущенные в среде приложения могут получать к ним доступ, включая конечные точки, доступные с помощью подключения типа [сеть — сеть][SiteToSite] и канала [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="489e6-140">Once an App Service Environment is joined to the same virtual network as the internal services, apps running in the environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="489e6-141">Дополнительные сведения о том, как среды службы приложений работают с виртуальными и локальными сетями, см. в статьях [Общие сведения об архитектуре сетевых сред службы приложений][NetworkArchitectureOverview], [Как управлять входящим трафиком в среде службы приложений][ControllingInboundTraffic] и [Безопасное подключение к серверным ресурсам из среды службы приложений][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="489e6-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult the following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting to Backends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="489e6-142">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="489e6-142">Getting started</span></span>
<span data-ttu-id="489e6-143">Чтобы приступить к работе со средами службы приложений, изучите статью [Создание среды службы приложений][HowToCreateAnAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="489e6-143">To get started with App Service Environments, see [How To Create An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="489e6-144">Все статьи и практические руководства, посвященные средам службы приложений, доступны в [файле сведений для сред службы приложений](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="489e6-144">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="489e6-145">Дополнительные сведения о платформе службы приложений Azure см. в статье [Что такое служба приложений Azure?][AzureAppService]</span><span class="sxs-lookup"><span data-stu-id="489e6-145">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="489e6-146">Обзор сетевой архитектуры среды службы приложений представлен в статье [Общие сведения об архитектуре сетевых сред службы приложений][NetworkArchitectureOverview].</span><span class="sxs-lookup"><span data-stu-id="489e6-146">For an overview of the App Service Environment network architecture, see the [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="489e6-147">Дополнительные сведения об использовании среды службы приложений с ExpressRoute см. в статье [Сведения о конфигурации сети для сред службы приложений с ExpressRoute][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="489e6-147">For details on using an App Service Environment with ExpressRoute, see the following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

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


