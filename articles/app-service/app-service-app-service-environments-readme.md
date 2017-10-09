---
title: "aaaApp среды службы | Документы Microsoft"
description: "Сведения о том, что из себя представляет среда службы приложений. TooApp введение среды службы."
keywords: "среда службы приложений Azure, виртуальная сеть, безопасная работа в сети"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 1db5c057-3c56-4537-b580-cdd21fe3f3a7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: stefsch
ms.openlocfilehash: 1b59fed4e5a72d4c4805e1dca203747e07e77103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="b836c-105">Документация по среде службы приложений</span><span class="sxs-lookup"><span data-stu-id="b836c-105">App Service Environment Documentation</span></span>
<span data-ttu-id="b836c-106">Среда службы приложений — это план обслуживания [Премиум][PremiumTier] в службе приложений Azure. Она обеспечивает полностью изолированную и выделенную среду для безопасного выполнения приложений службы приложений Azure в большом масштабе, включая [веб-приложения][WebApps], [мобильные приложения][MobileApps] и [приложения API][APIApps].</span><span class="sxs-lookup"><span data-stu-id="b836c-106">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="b836c-107">Среда службы приложений идеально подходит для рабочих нагрузок приложений, требующих выполнения указанных ниже условий.</span><span class="sxs-lookup"><span data-stu-id="b836c-107">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="b836c-108">Очень большой масштаб</span><span class="sxs-lookup"><span data-stu-id="b836c-108">Very high scale</span></span>
* <span data-ttu-id="b836c-109">Изоляция и безопасный доступ к сети</span><span class="sxs-lookup"><span data-stu-id="b836c-109">Isolation and secure network access</span></span>

<span data-ttu-id="b836c-110">Клиенты могут создавать несколько сред службы приложений как в одном, так и в нескольких регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="b836c-110">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="b836c-111">Благодаря этому среды службы приложений идеально подходят для горизонтально масштабируемых уровней приложений без учета состояний, поддерживающих большие рабочие нагрузки RPS.</span><span class="sxs-lookup"><span data-stu-id="b836c-111">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="b836c-112">Среды службы приложений — это изолированное toorunning только одного клиента приложения и всегда развертываются в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b836c-112">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="b836c-113">Клиенты могут детально управлять входящим и исходящим сетевым трафиком приложений, используя [группы безопасности сети][NetworkSecurityGroups], а</span><span class="sxs-lookup"><span data-stu-id="b836c-113">Customers have fine-grained control over both inbound and outbound application network traffic using [network security groups][NetworkSecurityGroups].</span></span>  <span data-ttu-id="b836c-114">Приложения можно также установить высокоскоростной безопасные соединения по корпоративным ресурсам локальной tooon виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="b836c-114">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="b836c-115">Приложения часто требуется tooaccess корпоративным ресурсам, например внутренними базами данных и веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b836c-115">Apps frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="b836c-116">Приложения, работающие в средах службы приложений, могут получать доступ к ресурсам через VPN-подключение типа [сеть — сеть][SiteToSite] или через канал [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="b836c-116">Apps running on App Service Environments can access resources reachable via [Site-to-Site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* [<span data-ttu-id="b836c-117">Введение в среду службы приложений</span><span class="sxs-lookup"><span data-stu-id="b836c-117">What is an App Service Environment?</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
* [<span data-ttu-id="b836c-118">Создание среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="b836c-118">Creating an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="b836c-119">Создание веб-приложения в среде служб приложений</span><span class="sxs-lookup"><span data-stu-id="b836c-119">Creating Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="b836c-120">Using an Internal Load Balancer with an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="b836c-120">Creating and Using an Internal Load Balancer with App Service Environments</span></span>](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [<span data-ttu-id="b836c-121">Настройка среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="b836c-121">Configuring an App Service Environment</span></span>](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [<span data-ttu-id="b836c-122">Масштабирование приложений в среде службы приложений</span><span class="sxs-lookup"><span data-stu-id="b836c-122">Scaling Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [<span data-ttu-id="b836c-123">Общие сведения об архитектуре сетевых сред службы приложений</span><span class="sxs-lookup"><span data-stu-id="b836c-123">Network Security and Architecture</span></span>](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a><span data-ttu-id="b836c-124">Инструкции</span><span class="sxs-lookup"><span data-stu-id="b836c-124">How To's</span></span>
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a><span data-ttu-id="b836c-125">Видеоролики</span><span class="sxs-lookup"><span data-stu-id="b836c-125">Videos</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]



<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
