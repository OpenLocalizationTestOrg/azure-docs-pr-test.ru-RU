---
title: "Файл сведений о среде службы приложений Azure"
description: "В этой статье приводится список документации по среде службы приложений Azure."
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 5b1362854dbc3b0098718bd2ea3cffb06366000c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="1f43f-103">Документация по среде службы приложений</span><span class="sxs-lookup"><span data-stu-id="1f43f-103">App Service environment documentation</span></span>
 <span data-ttu-id="1f43f-104">Среда службы приложений Azure — это компонент службы приложений Azure, предоставляющий полностью изолированную и выделенную среду для безопасного выполнения приложений службы приложений в большом масштабе.</span><span class="sxs-lookup"><span data-stu-id="1f43f-104">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="1f43f-105">В ней можно размещать свои [веб-приложения][webapps], [мобильные приложения][mobileapps], [приложения API][APIApps] и [функции][Functions].</span><span class="sxs-lookup"><span data-stu-id="1f43f-105">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIApps], and [functions][Functions].</span></span>

<span data-ttu-id="1f43f-106">Среды службы приложений (ASE) идеально подходят для рабочих нагрузок приложений, требующих выполнения указанных ниже условий.</span><span class="sxs-lookup"><span data-stu-id="1f43f-106">App Service environments (ASEs) are ideal for application workloads that require:</span></span>

* <span data-ttu-id="1f43f-107">Очень большой масштаб.</span><span class="sxs-lookup"><span data-stu-id="1f43f-107">Very high scale.</span></span>
* <span data-ttu-id="1f43f-108">Изоляция и безопасный доступ к сети.</span><span class="sxs-lookup"><span data-stu-id="1f43f-108">Isolation and secure network access.</span></span>

<span data-ttu-id="1f43f-109">Клиенты могут создавать несколько сред ASE в одном или в нескольких регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="1f43f-109">Customers can create multiple ASEs within a single Azure region and across multiple Azure regions.</span></span> <span data-ttu-id="1f43f-110">Благодаря этой гибкости среды ASE идеально подходят для горизонтально масштабируемых уровней приложений без учета состояний, поддерживающих большие рабочие нагрузки RPS.</span><span class="sxs-lookup"><span data-stu-id="1f43f-110">This versatility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="1f43f-111">Среды ASE изолированы, позволяют запускать приложения только одного клиента и всегда развернуты в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="1f43f-111">ASEs are isolated to running only a single customer's applications and are always deployed into an Azure virtual network.</span></span> <span data-ttu-id="1f43f-112">Клиенты могут детально управлять входящим и исходящим сетевым трафиком приложений, используя [группы безопасности сети][NSGs], а</span><span class="sxs-lookup"><span data-stu-id="1f43f-112">Customers have fine-grained control over inbound and outbound application network traffic by using [Network Security Groups][NSGs].</span></span> <span data-ttu-id="1f43f-113">приложения — создавать высокоскоростные безопасные подключения к локальным корпоративным ресурсам через виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="1f43f-113">Applications can also establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="1f43f-114">Приложениям также часто требуется доступ к корпоративным ресурсам, таким как внутренние базы данных и веб-службы.</span><span class="sxs-lookup"><span data-stu-id="1f43f-114">Apps frequently need to access corporate resources, such as internal databases and web services.</span></span> <span data-ttu-id="1f43f-115">Приложения, работающие в средах ASE, могут получать доступ к ресурсам через VPN-подключение типа [сеть — сеть][SiteToSite] или через канал [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="1f43f-115">Apps that run on ASEs can access resources via [site-to-site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* <span data-ttu-id="1f43f-116">[Введение в среду службы приложений][Intro]</span><span class="sxs-lookup"><span data-stu-id="1f43f-116">[What is an App Service environment?][Intro]</span></span>
* <span data-ttu-id="1f43f-117">[Создание среды службы приложений][MakeExternalASE]</span><span class="sxs-lookup"><span data-stu-id="1f43f-117">[Create an App Service environment][MakeExternalASE]</span></span>
* <span data-ttu-id="1f43f-118">[Создание и использование внутреннего балансировщика нагрузки со средой службы приложений][MakeILBASE]</span><span class="sxs-lookup"><span data-stu-id="1f43f-118">[Create an internal load balancer App Service environment][MakeILBASE]</span></span>
* <span data-ttu-id="1f43f-119">[Использование среды службы приложений][UsingASE]</span><span class="sxs-lookup"><span data-stu-id="1f43f-119">[Use an App Service environment][UsingASE]</span></span>
* <span data-ttu-id="1f43f-120">[Рекомендации по работе с сетями в среде службы приложений][ASENetwork]</span><span class="sxs-lookup"><span data-stu-id="1f43f-120">[Networking considerations and the App Service environment][ASENetwork]</span></span>
* <span data-ttu-id="1f43f-121">[Создание среды службы приложений с внутренней подсистемой балансировки нагрузки с помощью шаблонов Azure Resource Manager][MakeASEfromTemplate]</span><span class="sxs-lookup"><span data-stu-id="1f43f-121">[Create an App Service environment from a template][MakeASEfromTemplate]</span></span>


## <a name="videos"></a><span data-ttu-id="1f43f-122">Видеоролики</span><span class="sxs-lookup"><span data-stu-id="1f43f-122">Videos</span></span>
<span data-ttu-id="1f43f-123">Создание современной корпоративной платформы PaaS с помощью службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="1f43f-123">Master Modern PaaS for the Enterprise with Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

<span data-ttu-id="1f43f-124">Развертывание высокомасштабируемых и защищенных приложений</span><span class="sxs-lookup"><span data-stu-id="1f43f-124">Deploying Highly Scalable and Secure Apps</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

<span data-ttu-id="1f43f-125">Выполнение корпоративных веб-приложений и мобильных приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="1f43f-125">Running Enterprise Web and Mobile Apps on Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="1f43f-126">Среда службы приложений версии 1</span><span class="sxs-lookup"><span data-stu-id="1f43f-126">App Service Environment v1</span></span> ##
<span data-ttu-id="1f43f-127">Существует две версии среды службы приложений: ASEv1 и ASEv2.</span><span class="sxs-lookup"><span data-stu-id="1f43f-127">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="1f43f-128">Сведения об ASEv1 см. в статье [Документация по среде службы приложений][ASEv1README].</span><span class="sxs-lookup"><span data-stu-id="1f43f-128">For information on ASEv1, see [App Service Environment v1 documentation][ASEv1README].</span></span>


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
