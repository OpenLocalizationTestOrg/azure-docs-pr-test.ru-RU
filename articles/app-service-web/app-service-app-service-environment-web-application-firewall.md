---
title: "Настройка брандмауэра веб-приложения (WAF) для среды службы приложений"
description: "Узнайте, как настроить брандмауэр веб-приложения перед средой службы приложений."
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
ms.openlocfilehash: 3e9e9fa4ddab60a467e8aa793ec0ca269b0bc4e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="65066-103">Настройка брандмауэра веб-приложения (WAF) для среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="65066-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="65066-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="65066-104">Overview</span></span>
<span data-ttu-id="65066-105">Брандмауэры веб-приложений, например [Barracuda для Azure](https://www.barracuda.com/programs/azure), который доступен в [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/), помогают защитить веб-приложения, проверяя входящий веб-трафик и блокируя атаки (путем внедрения кода SQL), межсайтовые скрипты, загрузку вредоносных программ, а также распределенные атаки типа "отказ в обслуживании" и другие атаки.</span><span class="sxs-lookup"><span data-stu-id="65066-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="65066-106">Также они проверяют ответы от внутренних веб-серверов для предотвращения потери данных (DLP).</span><span class="sxs-lookup"><span data-stu-id="65066-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="65066-107">В сочетании с изоляцией и дополнительным масштабированием, предоставляемым средами службы приложений, это обеспечивает идеальную среду для размещения важных коммерческих веб-приложений с большим трафиком, способных противостоять вредоносным запросам.</span><span class="sxs-lookup"><span data-stu-id="65066-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="65066-108">Настройка</span><span class="sxs-lookup"><span data-stu-id="65066-108">Setup</span></span>
<span data-ttu-id="65066-109">Мы настроим среду службы приложений за несколькими экземплярами Barracuda WAF с равномерной нагрузкой, чтобы только трафик от WAF мог достичь среды службы приложений. Так среда не будет доступна из промежуточной подсети.</span><span class="sxs-lookup"><span data-stu-id="65066-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span></span> <span data-ttu-id="65066-110">Мы также настроим диспетчер трафика Azure перед экземплярами Barracuda WAF, чтобы распределить нагрузку между несколькими центрами обработки данных и регионами Azure.</span><span class="sxs-lookup"><span data-stu-id="65066-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="65066-111">Общая схема настройки выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="65066-111">A high level diagram of the setup would look like what is shown below.</span></span>

![Архитектура][Architecture] 

> <span data-ttu-id="65066-113">Примечание. С появлением [поддержки ILB в среде службы приложений](app-service-environment-with-internal-load-balancer.md) вы можете закрыть доступ к среде службы приложений из промежуточной подсети, чтобы она была доступна только для частной сети.</span><span class="sxs-lookup"><span data-stu-id="65066-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="65066-114">Настройка среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="65066-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="65066-115">Инструкции по настройке среды службы приложений см. в соответствующей [документации](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="65066-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="65066-116">После создания среды службы приложений в ней можно создать [веб-приложения](app-service-web-overview.md), [приложения API](../app-service-api/app-service-api-apps-why-best-platform.md) и [мобильные приложения](../app-service-mobile/app-service-mobile-value-prop.md), которые будут защищены брандмауэром веб-приложения, который мы настроим в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="65066-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="65066-117">Настройка облачной службы Barracuda WAF</span><span class="sxs-lookup"><span data-stu-id="65066-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="65066-118">У нас есть [подробная статья](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) о развертывании Barracuda WAF на виртуальной машине в Azure.</span><span class="sxs-lookup"><span data-stu-id="65066-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="65066-119">Так как нам нужна отказоустойчивость и отсутствие единой точки отказа, необходимо развернуть по крайней мере 2 экземпляра виртуальных машин с WAF в той же облачной службе, следуя этим инструкциям.</span><span class="sxs-lookup"><span data-stu-id="65066-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="65066-120">Добавление конечных точек в облачной службе</span><span class="sxs-lookup"><span data-stu-id="65066-120">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="65066-121">После создания в облачной службе двух и более экземпляров виртуальных машин с WAF используйте [классический портал Azure](https://portal.azure.com/) , чтобы добавить конечные точки HTTP и HTTPS, которые будут использоваться вашим приложением, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="65066-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span></span>

![Настройка конечной точки][ConfigureEndpoint]

<span data-ttu-id="65066-123">Если в приложениях используются другие конечные точки, их также необходимо добавить в этот список.</span><span class="sxs-lookup"><span data-stu-id="65066-123">If your applications use other endpoints, make sure to add those to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="65066-124">Настройка Barracuda WAF через портал управления</span><span class="sxs-lookup"><span data-stu-id="65066-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="65066-125">Barracuda WAF использует TCP-порт 8000 для настройки с помощью портала управления.</span><span class="sxs-lookup"><span data-stu-id="65066-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="65066-126">Так как имеется несколько экземпляров ВМ WAF, необходимо повторить приведенные здесь шаги для каждого экземпляра ВМ.</span><span class="sxs-lookup"><span data-stu-id="65066-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span></span> 

> <span data-ttu-id="65066-127">Примечание. После завершения настройки WAF удалите конечную точку TCP/8000 из всех ВМ WAF для безопасности вашего WAF.</span><span class="sxs-lookup"><span data-stu-id="65066-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="65066-128">Добавьте конечную точку управления, как показано на рисунке ниже, для настройки вашего Barracuda WAF.</span><span class="sxs-lookup"><span data-stu-id="65066-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span></span>

![Добавление конечной точки управления][AddManagementEndpoint]

<span data-ttu-id="65066-130">С помощью браузера перейдите к конечной точке управления в своей облачной службе.</span><span class="sxs-lookup"><span data-stu-id="65066-130">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="65066-131">Если имя вашей облачной службы test.cloudapp.net, доступ к этой конечной точке можно получить по адресу http://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="65066-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="65066-132">Отобразится страница входа (как на рисунке ниже), через которую можно войти с помощью учетных данных, которые вы указали на этапе установки WAF ВМ.</span><span class="sxs-lookup"><span data-stu-id="65066-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span></span>

![Страница управления входом][ManagementLoginPage]

<span data-ttu-id="65066-134">После входа вы увидите панель мониторинга (как на рисунке ниже) с базовой статистикой о защите WAF.</span><span class="sxs-lookup"><span data-stu-id="65066-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span></span>

![Панель управления][ManagementDashboard]

<span data-ttu-id="65066-136">На вкладке "Службы" можно настроить WAF для защиты служб.</span><span class="sxs-lookup"><span data-stu-id="65066-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="65066-137">Дополнительные сведения о настройке WAF Barracuda можно найти в соответствующей [документации](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="65066-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="65066-138">В примере ниже приведена настройка веб-приложения Azure, обслуживающего трафик по протоколам HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="65066-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Управление: добавление служб][ManagementAddServices]

> <span data-ttu-id="65066-140">Примечание. В зависимости от настроек ваших приложений и функций, используемых в среде службы приложений, будет необходимо перенаправлять трафик для TCP портов, отличных от 80 и 443, например при наличии настройки IP SSL для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="65066-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="65066-141">Список сетевых портов, используемых в средах службы приложений, см. в разделе "Сетевые порты, используемые в среде службы приложений" [документации по управлению входящим трафиком](app-service-app-service-environment-control-inbound-traffic.md).</span><span class="sxs-lookup"><span data-stu-id="65066-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="65066-142">Настройка диспетчера трафика Microsoft Azure (необязательно)</span><span class="sxs-lookup"><span data-stu-id="65066-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="65066-143">Если приложение доступно в нескольких регионах, необходимо сбалансировать нагрузку с помощью [диспетчера трафика Azure](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65066-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="65066-144">Для этого можно добавить конечную точку на [классическом портале Azure](https://manage.azure.com) с помощью имени облачной службы для вашего WAF в профиле диспетчера трафика, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="65066-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span></span> 

![Конечная точка диспетчера трафика][TrafficManagerEndpoint]

<span data-ttu-id="65066-146">Если приложение требует проверки подлинности, убедитесь, что у вас есть ресурсы для проверки доступности приложения, которые не требуют проверки подлинности через диспетчер трафика.</span><span class="sxs-lookup"><span data-stu-id="65066-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="65066-147">URL-адрес можно указать в разделе "Настройка" [классического портала Azure](https://manage.azure.com) , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="65066-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Настройка диспетчера трафика][ConfigureTrafficManager]

<span data-ttu-id="65066-149">Для перенаправления проверочных запросов диспетчера трафика из WAF в приложение необходимо установить Website Translations на Barracuda WAF для перенаправления трафика к приложению, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="65066-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span></span>

![Переводы веб-сайта][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="65066-151">Защита трафика в среде службы приложений с помощью групп безопасности сети (NSG)</span><span class="sxs-lookup"><span data-stu-id="65066-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="65066-152">Дополнительные сведения об ограничении трафика в среду службы приложений только от WAF с помощью виртуального IP-адреса облачной службы см. в [документации по управлению входящим трафиком](app-service-app-service-environment-control-inbound-traffic.md).</span><span class="sxs-lookup"><span data-stu-id="65066-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="65066-153">Ниже приведен пример команды Powershell для выполнения этой задачи для TCP-порта 80.</span><span class="sxs-lookup"><span data-stu-id="65066-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="65066-154">Замените SourceAddressPrefix на виртуальный IP-адрес (VIP) облачной службы WAF.</span><span class="sxs-lookup"><span data-stu-id="65066-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="65066-155">Примечание. VIP облачной службы изменится, если удалить и повторно создать облачную службу.</span><span class="sxs-lookup"><span data-stu-id="65066-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="65066-156">Не забудьте после этого обновить IP-адрес в группе ресурсов сети.</span><span class="sxs-lookup"><span data-stu-id="65066-156">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
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
