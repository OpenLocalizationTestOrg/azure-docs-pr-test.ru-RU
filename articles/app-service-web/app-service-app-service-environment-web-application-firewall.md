---
title: "aaaConfiguring брандмауэра приложений Web (WAF) для среды службы приложений"
description: "Узнайте, как брандмауэре tooconfigure веб-приложения перед среды службы приложений."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="245eb-103">Настройка брандмауэра веб-приложения (WAF) для среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="245eb-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="245eb-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="245eb-104">Overview</span></span>
<span data-ttu-id="245eb-105">Веб-приложения брандмауэров как hello [WAF Barracuda для Azure](https://www.barracuda.com/programs/azure) , которое доступно на hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) помогает защитить веб-приложений путем проверки tooblock web входящий трафик SQL включению, межсайтовых сценариев, вредоносных программ передач & приложения DDoS и других атак.</span><span class="sxs-lookup"><span data-stu-id="245eb-105">Web application firewalls like hello [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic tooblock SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="245eb-106">Он также проверяет hello ответы от hello серверной части веб-серверов для защиты от потери данных (DLP).</span><span class="sxs-lookup"><span data-stu-id="245eb-106">It also inspects hello responses from hello back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="245eb-107">В сочетании с изоляции hello и дополнительных масштабирования среды службы приложений, предоставляемые, это обеспечивает идеальную среду toohost деловые критических веб-приложения, которым нужны toowithstand вредоносных запросов и большого объема трафика.</span><span class="sxs-lookup"><span data-stu-id="245eb-107">Combined with hello isolation and additional scaling provided by App Service Environments, this provides an ideal environment toohost business critical web applications that need toowithstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="245eb-108">Настройка</span><span class="sxs-lookup"><span data-stu-id="245eb-108">Setup</span></span>
<span data-ttu-id="245eb-109">Для этого документа, которые мы настроить нашей среды службы приложений за несколько нагрузки равномерно экземпляров Barracuda WAF, чтобы трафик только с hello WAF может достигать hello среды службы приложений, и он не будет доступен из сети Периметра hello.</span><span class="sxs-lookup"><span data-stu-id="245eb-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from hello WAF can reach hello App Service Environment and it will not be accessible from hello DMZ.</span></span> <span data-ttu-id="245eb-110">Мы также получат диспетчера трафика Azure перед нашей Barracuda WAF экземпляров tooload баланс между центрами обработки данных Azure и регионов.</span><span class="sxs-lookup"><span data-stu-id="245eb-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances tooload balance across Azure data centers and regions.</span></span> <span data-ttu-id="245eb-111">Высокоуровневая схема установки hello выглядит следующим образом показанной ниже.</span><span class="sxs-lookup"><span data-stu-id="245eb-111">A high level diagram of hello setup would look like what is shown below.</span></span>

![Архитектура][Architecture] 

> <span data-ttu-id="245eb-113">Примечание: С введением hello [ILB поддержка среды службы приложений](app-service-environment-with-internal-load-balancer.md), можно настроить toobe hello ASE недоступны из hello DMZ и быть только доступные toohello частной сети.</span><span class="sxs-lookup"><span data-stu-id="245eb-113">Note: With hello introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure hello ASE toobe inaccessible from hello DMZ and only be available toohello private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="245eb-114">Настройка среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="245eb-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="245eb-115">tooconfigure среды службы приложений ссылаться слишком[нашей документации](app-service-web-how-to-create-an-app-service-environment.md) по теме hello.</span><span class="sxs-lookup"><span data-stu-id="245eb-115">tooconfigure an App Service Environment refer too[our documentation](app-service-web-how-to-create-an-app-service-environment.md) on hello subject.</span></span> <span data-ttu-id="245eb-116">После создания среды службы приложений, можно создать [веб-приложений](app-service-web-overview.md), [приложения API](../app-service-api/app-service-api-apps-why-best-platform.md) и [мобильные приложения](../app-service-mobile/app-service-mobile-value-prop.md) в этой среде, который будет защищать за hello WAF мы Настройте в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="245eb-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind hello WAF we configure in hello next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="245eb-117">Настройка облачной службы Barracuda WAF</span><span class="sxs-lookup"><span data-stu-id="245eb-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="245eb-118">У нас есть [подробная статья](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) о развертывании Barracuda WAF на виртуальной машине в Azure.</span><span class="sxs-lookup"><span data-stu-id="245eb-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="245eb-119">Но так как мы должны избыточность и вводит единую точку сбоя, необходимо, чтобы экземпляр WAF toodeploy по крайней мере 2 виртуальных машин в hello одной облачной службе, когда выполнение этих инструкций.</span><span class="sxs-lookup"><span data-stu-id="245eb-119">But because we want redundancy and not introduce a single point of failure, you want toodeploy at least 2 WAF instance VMs into hello same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-toocloud-service"></a><span data-ttu-id="245eb-120">Добавление tooCloud конечные точки службы</span><span class="sxs-lookup"><span data-stu-id="245eb-120">Adding Endpoints tooCloud Service</span></span>
<span data-ttu-id="245eb-121">Когда имеется 2 или несколько виртуальных Машин WAF экземпляров в облачной службе можно использовать hello [портал Azure](https://portal.azure.com/) tooadd HTTP и HTTPS конечные точки, используемые вашим приложением, как показано в приведенном ниже рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="245eb-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use hello [Azure portal](https://portal.azure.com/) tooadd HTTP and HTTPS endpoints that are used by your application as shown in hello image below.</span></span>

![Настройка конечной точки][ConfigureEndpoint]

<span data-ttu-id="245eb-123">Если приложения используют другие конечные точки, создайте список этих toothis, также убедиться, что tooadd.</span><span class="sxs-lookup"><span data-stu-id="245eb-123">If your applications use other endpoints, make sure tooadd those toothis list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="245eb-124">Настройка Barracuda WAF через портал управления</span><span class="sxs-lookup"><span data-stu-id="245eb-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="245eb-125">Barracuda WAF использует TCP-порт 8000 для настройки с помощью портала управления.</span><span class="sxs-lookup"><span data-stu-id="245eb-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="245eb-126">Поскольку у нас есть несколько экземпляров виртуальных машин WAF hello toorepeat hello при выполнении шагов потребуется для каждого экземпляра виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="245eb-126">Since we have multiple instances of hello WAF VMs you will need toorepeat hello steps here for each VM instance.</span></span> 

> <span data-ttu-id="245eb-127">Примечание: После завершения работы с конфигурацией WAF, удалите конечную точку TCP/8000 hello из всех вашей tookeep WAF виртуальных машин вашей WAF безопасного.</span><span class="sxs-lookup"><span data-stu-id="245eb-127">Note: Once you are done with WAF configuration, remove hello TCP/8000 endpoint from all your WAF VMs tookeep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="245eb-128">Добавьте конечную точку управления hello как показано на рисунке hello ниже tooconfigure вашей WAF Barracuda.</span><span class="sxs-lookup"><span data-stu-id="245eb-128">Add hello management endpoint as shown in hello image below tooconfigure your Barracuda WAF.</span></span>

![Добавление конечной точки управления][AddManagementEndpoint]

<span data-ttu-id="245eb-130">Используйте браузер конечная точка управления toobrowse toohello на облачной службы.</span><span class="sxs-lookup"><span data-stu-id="245eb-130">Use a browser toobrowse toohello management endpoint on your Cloud Service.</span></span> <span data-ttu-id="245eb-131">Если облачная служба вызывается test.cloudapp.net, доступ к этой конечной точке путем просмотра toohttp://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="245eb-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing toohttp://test.cloudapp.net:8000.</span></span> <span data-ttu-id="245eb-132">Должна появиться страница входа в систему, аналогичные показанным ниже можно выполнить вход с использованием учетных данных, указанный в фазу установки hello WAF виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="245eb-132">You should see a login page like below that you can login using credentials you specified in hello WAF VM setup phase.</span></span>

![Страница управления входом][ManagementLoginPage]

<span data-ttu-id="245eb-134">После входа вы увидите панель мониторинга как hello один hello рисунке ниже, будет представлять базовую статистику о hello WAF защиты.</span><span class="sxs-lookup"><span data-stu-id="245eb-134">Once you login you should see a dashboard as hello one in hello image below that will present basic statistics about hello WAF protection.</span></span>

![Панель управления][ManagementDashboard]

<span data-ttu-id="245eb-136">Нажав на вкладку "службы" hello позволит вам настроить вашей WAF для служб, которые он защищает.</span><span class="sxs-lookup"><span data-stu-id="245eb-136">Clicking on hello Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="245eb-137">Дополнительные сведения о настройке WAF Barracuda можно найти в соответствующей [документации](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="245eb-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="245eb-138">В примере hello ниже веб-приложение Azure обслуживающий трафика по протоколам HTTP и HTTPS настроена.</span><span class="sxs-lookup"><span data-stu-id="245eb-138">In hello example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Управление: добавление служб][ManagementAddServices]

> <span data-ttu-id="245eb-140">Примечание: В зависимости от того, как настроена приложения и какие функции используются в среде службы приложений, вам потребуется tooforward трафика для TCP-порты, отличные от 80 и 443, например если вы настроили IP SSL для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="245eb-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need tooforward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="245eb-141">Список сетевых портов, используемых в среде службы приложений, можно найти слишком[входящий трафик управления документации](app-service-app-service-environment-control-inbound-traffic.md) раздел сетевые порты.</span><span class="sxs-lookup"><span data-stu-id="245eb-141">For a list of network ports used in App Service Environments, please refer too[Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="245eb-142">Настройка диспетчера трафика Microsoft Azure (необязательно)</span><span class="sxs-lookup"><span data-stu-id="245eb-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="245eb-143">Если приложение будет доступно в нескольких регионах, то требуется баланс tooload их за [диспетчера трафика Azure](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="245eb-143">If your application is available in multiple regions, then you would want tooload balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="245eb-144">toodo, поэтому можно добавить конечную точку в hello [классический портал Azure](https://manage.azure.com) с помощью hello имя облачной службы для вашего WAF в профиле диспетчера трафика hello, как показано в приведенном ниже рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="245eb-144">toodo so you can add an endpoint in hello [Azure classic portal](https://manage.azure.com) using hello Cloud Service name for your WAF in hello Traffic Manager profile as shown in hello image below.</span></span> 

![Конечная точка диспетчера трафика][TrafficManagerEndpoint]

<span data-ttu-id="245eb-146">Если приложение требует проверки подлинности, убедитесь, что у вас есть некоторые ресурсы, не требуется проверка подлинности для tooping диспетчера трафика для доступности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="245eb-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager tooping for hello availability of your application.</span></span> <span data-ttu-id="245eb-147">Вы можете настроить URL-адресом hello в разделе Настройка hello в hello [классический портал Azure](https://manage.azure.com) как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="245eb-147">You can configure hello URL under hello Configure section on hello [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Настройка диспетчера трафика][ConfigureTrafficManager]

<span data-ttu-id="245eb-149">tooforward hello диспетчера трафика запросы проверки связи от приложения tooyour WAF, Barracuda WAF tooforward трафика tooyour приложения, как показано в следующем примере hello должны переводы toosetup веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="245eb-149">tooforward hello Traffic Manager pings from your WAF tooyour application, you need toosetup Website Translations on your Barracuda WAF tooforward traffic tooyour application as shown in hello example below.</span></span>

![Переводы веб-сайта][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="245eb-151">Обеспечение безопасности трафика tooApp службы среды с помощью сетевой безопасности группы (NSG)</span><span class="sxs-lookup"><span data-stu-id="245eb-151">Securing Traffic tooApp Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="245eb-152">Выполните hello [документации входящий трафик управления](app-service-app-service-environment-control-inbound-traffic.md) для сведений об ограничении трафика tooyour среды службы приложений из hello WAF только с помощью адреса hello виртуальный IP-адрес облачной службы.</span><span class="sxs-lookup"><span data-stu-id="245eb-152">Follow hello [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic tooyour App Service Environment from hello WAF only by using hello VIP address of your Cloud Service.</span></span> <span data-ttu-id="245eb-153">Ниже приведен пример команды Powershell для выполнения этой задачи для TCP-порта 80.</span><span class="sxs-lookup"><span data-stu-id="245eb-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="245eb-154">Замените hello SourceAddressPrefix hello Virtual IP Address (VIP) для вашей WAF облачной службы.</span><span class="sxs-lookup"><span data-stu-id="245eb-154">Replace hello SourceAddressPrefix with hello Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="245eb-155">Примечание: hello виртуальный IP-адрес облачной службы изменится, если удалить и повторно создать hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="245eb-155">Note: hello VIP of your Cloud Service will change when you delete and re-create hello Cloud Service.</span></span> <span data-ttu-id="245eb-156">Убедитесь, что tooupdate hello IP-адрес в группе ресурсов сети hello после этого.</span><span class="sxs-lookup"><span data-stu-id="245eb-156">Make sure tooupdate hello IP address in hello Network Resource group once you do so.</span></span> 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
