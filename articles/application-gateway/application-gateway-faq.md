---
title: "вопросы и ответы для шлюза приложения Azure aaaFrequently | Документы Microsoft"
description: "Эта страница содержит ответы toofrequently вопросы и ответы о шлюзе приложения Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="0d710-103">Часто задаваемые вопросы о шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="0d710-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="0d710-104">Общие сведения</span><span class="sxs-lookup"><span data-stu-id="0d710-104">General</span></span>

<span data-ttu-id="0d710-105">**В. Что такое шлюз приложений?**</span><span class="sxs-lookup"><span data-stu-id="0d710-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="0d710-106">Шлюз приложений Azure является контроллером доставки приложений (ADC) как услуг, предлагающих для приложений разные функции балансировки нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="0d710-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="0d710-107">Это высокодоступная и масштабируемая служба, которая полностью управляется Azure.</span><span class="sxs-lookup"><span data-stu-id="0d710-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="0d710-108">**В. Какие функции поддерживает шлюз приложений?**</span><span class="sxs-lookup"><span data-stu-id="0d710-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="0d710-109">Шлюз приложений поддерживает SSL разгрузки и окончания tooend SSL, брандмауэр веб-приложения, сходство сеансов на основе файлов cookie, URL-адрес основанную на пути маршрутизации, размещение нескольких сайта и другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="0d710-109">Application Gateway supports SSL offloading and end tooend SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="0d710-110">Полный список поддерживаемых функций см. на сайте [tooApplication введение шлюза](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="0d710-110">For a full list of supported features, visit [Introduction tooApplication Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="0d710-111">**В. Что такое hello различие между шлюзом приложения и подсистемы балансировки нагрузки Azure?**</span><span class="sxs-lookup"><span data-stu-id="0d710-111">**Q. What is hello difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="0d710-112">Шлюз приложений — балансировщик нагрузки уровня 7. Это означает, что он работает только с веб-трафиком (HTTP, HTTPS и WebSocket).</span><span class="sxs-lookup"><span data-stu-id="0d710-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="0d710-113">Он поддерживает такие функции, как завершение SSL-подключений, сопоставление сеансов на основе файлов cookie и циклический перебор для распределения нагрузки трафика.</span><span class="sxs-lookup"><span data-stu-id="0d710-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="0d710-114">С балансировщиком нагрузки доступна балансировка трафика уровня 4 (протоколы TCP и UDP).</span><span class="sxs-lookup"><span data-stu-id="0d710-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="0d710-115">**В. Какие протоколы поддерживает шлюз приложений?**</span><span class="sxs-lookup"><span data-stu-id="0d710-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="0d710-116">Шлюз приложений поддерживает протоколы HTTP, HTTPS и WebSocket.</span><span class="sxs-lookup"><span data-stu-id="0d710-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="0d710-117">**В. Какие ресурсы в настоящее время поддерживаются как часть серверного пула?**</span><span class="sxs-lookup"><span data-stu-id="0d710-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="0d710-118">Внутренние пулы могут состоять из сетевых адаптеров, масштабируемых наборов виртуальных машин, общедоступных IP-адресов, внутренних IP-адресов, полных доменных имен и таких мультитенантых серверных частей, как веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="0d710-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="0d710-119">Приложения шлюзов, которые члены серверной пул не привязан tooan группы доступности.</span><span class="sxs-lookup"><span data-stu-id="0d710-119">Application Gateway backend pool members are not tied tooan availability set.</span></span> <span data-ttu-id="0d710-120">Они могут располагаться в кластерах, центрах обработки данных или за пределами портала Azure, пока у них есть возможность подключения по IP.</span><span class="sxs-lookup"><span data-stu-id="0d710-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="0d710-121">**В. Какие регионы доступна служба hello в?**</span><span class="sxs-lookup"><span data-stu-id="0d710-121">**Q. What regions is hello service available in?**</span></span>

<span data-ttu-id="0d710-122">Шлюз приложений доступен во всех регионах глобальной платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="0d710-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="0d710-123">Он также доступен в [Azure для Китая](https://www.azure.cn/) и [Azure для государственных организаций](https://azure.microsoft.com/en-us/overview/clouds/government/).</span><span class="sxs-lookup"><span data-stu-id="0d710-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="0d710-124">**В. Это специальное развертывание для подписки или общее для всех клиентов?**</span><span class="sxs-lookup"><span data-stu-id="0d710-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="0d710-125">Шлюз приложений — это специальное развертывание в вашей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0d710-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="0d710-126">**В. Поддерживается ли перенаправление протоколов HTTP -> HTTPS?**</span><span class="sxs-lookup"><span data-stu-id="0d710-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="0d710-127">Перенаправление поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0d710-127">Redirection is supported.</span></span> <span data-ttu-id="0d710-128">Посетите [Обзор перенаправления шлюза приложения](application-gateway-redirect-overview.md) toolearn дополнительные.</span><span class="sxs-lookup"><span data-stu-id="0d710-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn more.</span></span>

<span data-ttu-id="0d710-129">**В. В каком порядке обрабатываются прослушиватели?**</span><span class="sxs-lookup"><span data-stu-id="0d710-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="0d710-130">Прослушиватели, обрабатываются в порядке hello, в котором они отображаются.</span><span class="sxs-lookup"><span data-stu-id="0d710-130">Listeners are processed in hello order they are shown.</span></span> <span data-ttu-id="0d710-131">Поэтому если основной прослушиватель соответствует поступившему запросу, он обработает этот запрос первым.</span><span class="sxs-lookup"><span data-stu-id="0d710-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="0d710-132">Прослушиватели нескольких сайтов должны быть настроены перед трафика tooensure основные прослушивателя — перенаправленное toohello правильный серверной части.</span><span class="sxs-lookup"><span data-stu-id="0d710-132">Multi-site listeners should be configured before a basic listener tooensure traffic is routed toohello correct back-end.</span></span>

<span data-ttu-id="0d710-133">**В. Где найти IP-адрес и DNS-имя шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="0d710-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="0d710-134">При использовании общедоступный IP-адрес в качестве конечной точки, эти сведения можно найти на hello открытого ресурса IP-адреса или на страницу обзора hello для hello шлюза приложения hello портала.</span><span class="sxs-lookup"><span data-stu-id="0d710-134">When using a public IP address as an endpoint, this information can be found on hello public IP address resource or on hello Overview page for hello Application Gateway in hello portal.</span></span> <span data-ttu-id="0d710-135">Для внутренних IP-адресов это можно найти на странице Обзор hello.</span><span class="sxs-lookup"><span data-stu-id="0d710-135">For internal IP addresses, this can be found on hello Overview page.</span></span>

<span data-ttu-id="0d710-136">**В. Hello IP-адрес или DNS изменяется за время жизни hello hello шлюз приложений?**</span><span class="sxs-lookup"><span data-stu-id="0d710-136">**Q. Does hello IP or DNS change over hello lifetime of hello Application Gateway?**</span></span>

<span data-ttu-id="0d710-137">Hello виртуальных IP-адресов можно изменить при остановке и запуске клиентом hello hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="0d710-137">hello VIP can change if hello gateway is stopped and started by hello customer.</span></span> <span data-ttu-id="0d710-138">над жизненным циклом hello шлюза hello Hello DNS, связанной со шлюзом приложений не изменяется.</span><span class="sxs-lookup"><span data-stu-id="0d710-138">hello DNS associated with Application Gateway does not change over hello lifecycle of hello gateway.</span></span> <span data-ttu-id="0d710-139">По этой причине рекомендуется toouse псевдоним CNAME и укажите в нем toohello DNS-адрес шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0d710-139">For this reason, it is recommended toouse a CNAME alias and point it toohello DNS address of hello Application Gateway.</span></span>

<span data-ttu-id="0d710-140">**В. Поддерживает ли шлюз приложений статические IP-адреса?**</span><span class="sxs-lookup"><span data-stu-id="0d710-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="0d710-141">Нет, шлюз приложений не поддерживает статические общедоступные IP-адреса, но поддерживает статические внутренние.</span><span class="sxs-lookup"><span data-stu-id="0d710-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="0d710-142">**В. Шлюз приложений поддерживает несколько общих IP-адресов для hello шлюза?**</span><span class="sxs-lookup"><span data-stu-id="0d710-142">**Q. Does Application Gateway support multiple public IPs on hello gateway?**</span></span>

<span data-ttu-id="0d710-143">Шлюз приложений поддерживает только один общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0d710-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="0d710-144">**В. Поддерживает ли шлюз приложений заголовки X-Forwarded-For?**</span><span class="sxs-lookup"><span data-stu-id="0d710-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="0d710-145">Да, шлюз приложений вставляет x перенаправленных-, пересылаемые proto x, и пересылаются порт x заголовков в запросе hello пересылаются toohello серверной части.</span><span class="sxs-lookup"><span data-stu-id="0d710-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into hello request forwarded toohello backend.</span></span> <span data-ttu-id="0d710-146">Hello формат для заголовка x перенаправленных для — список разделенных запятой IP: Port.</span><span class="sxs-lookup"><span data-stu-id="0d710-146">hello format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="0d710-147">Hello допустимые значения для пересылки proto x: http или https.</span><span class="sxs-lookup"><span data-stu-id="0d710-147">hello valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="0d710-148">Пересылаемые порт X указывает порт hello по запросу какие hello, достигнут на hello шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0d710-148">X-forwarded-port specifies hello port at which hello request reached at hello Application Gateway.</span></span>

<span data-ttu-id="0d710-149">**В. Как долго требуется toodeploy шлюза приложения? Работает ли шлюз приложений во время обновления?**</span><span class="sxs-lookup"><span data-stu-id="0d710-149">**Q. How long does it take toodeploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="0d710-150">Новые развертывания шлюза приложения может занять tooprovision too20 минут.</span><span class="sxs-lookup"><span data-stu-id="0d710-150">New Application Gateway deployments can take up too20 minutes tooprovision.</span></span> <span data-ttu-id="0d710-151">Изменения tooinstance размера или числа объектов не нарушают работу и шлюза hello остается активным в течение этого времени.</span><span class="sxs-lookup"><span data-stu-id="0d710-151">Changes tooinstance size/count are not disruptive, and hello gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="0d710-152">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="0d710-152">Configuration</span></span>

<span data-ttu-id="0d710-153">**В. Всегда ли шлюз приложений развертывается в виртуальной сети?**</span><span class="sxs-lookup"><span data-stu-id="0d710-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="0d710-154">Да, шлюз приложений всегда развертывается в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0d710-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="0d710-155">Эта подсеть может содержать только шлюзы приложений.</span><span class="sxs-lookup"><span data-stu-id="0d710-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="0d710-156">**В. Можно шлюз приложений обращение tooinstances за пределами его виртуальной сети?**</span><span class="sxs-lookup"><span data-stu-id="0d710-156">**Q. Can Application Gateway talk tooinstances outside its virtual network?**</span></span>

<span data-ttu-id="0d710-157">Шлюз приложения могут взаимодействовать tooinstances за пределами hello виртуальной сети, которая находится в, при условии, что имеется IP-подключения.</span><span class="sxs-lookup"><span data-stu-id="0d710-157">Application Gateway can talk tooinstances outside of hello virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="0d710-158">Если планируется toouse внутренних IP-адресов как члены серверной части пула, то оно требует [виртуальную сеть Пиринга](../virtual-network/virtual-network-peering-overview.md) или [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="0d710-158">If you plan toouse internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="0d710-159">**В. Можно ли развертывать все остальное в подсеть шлюза приложения hello**</span><span class="sxs-lookup"><span data-stu-id="0d710-159">**Q. Can I deploy anything else in hello Application Gateway subnet?**</span></span>

<span data-ttu-id="0d710-160">Нет, но вы можете развернуть другие шлюзы приложений в подсети hello.</span><span class="sxs-lookup"><span data-stu-id="0d710-160">No, but you can deploy other application gateways in hello subnet.</span></span>

<span data-ttu-id="0d710-161">**В. Группы безопасности сети поддерживает подсеть шлюза приложения hello?**</span><span class="sxs-lookup"><span data-stu-id="0d710-161">**Q. Are Network Security Groups supported on hello Application Gateway subnet?**</span></span>

<span data-ttu-id="0d710-162">Поддерживает сетевые группы безопасности в подсети шлюза приложения hello hello следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="0d710-162">Network Security Groups are supported on hello Application Gateway subnet with hello following restrictions:</span></span>

* <span data-ttu-id="0d710-163">Исключения могут быть помещены для входящего трафика на порты 65503 65534 для серверной работоспособности toowork правильно.</span><span class="sxs-lookup"><span data-stu-id="0d710-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health toowork correctly.</span></span>

* <span data-ttu-id="0d710-164">Исходящее подключение к Интернету не может быть заблокировано.</span><span class="sxs-lookup"><span data-stu-id="0d710-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="0d710-165">Необходимо разрешить трафик от hello AzureLoadBalancer тег.</span><span class="sxs-lookup"><span data-stu-id="0d710-165">Traffic from hello AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="0d710-166">**В. Что такое hello ограничения на использование шлюза приложений Можно ли увеличить эти ограничения?**</span><span class="sxs-lookup"><span data-stu-id="0d710-166">**Q. What are hello limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="0d710-167">Посетите [ограничения шлюза приложения](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello ограничения.</span><span class="sxs-lookup"><span data-stu-id="0d710-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limits.</span></span>

<span data-ttu-id="0d710-168">**В. Можно ли использовать шлюз приложений одновременно для внешнего и внутреннего трафика?**</span><span class="sxs-lookup"><span data-stu-id="0d710-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="0d710-169">Да, каждый шлюз приложений может иметь один внутренний IP-адрес и один внешний.</span><span class="sxs-lookup"><span data-stu-id="0d710-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="0d710-170">**В. Поддерживается ли пиринговая связь между виртуальными сетями?**</span><span class="sxs-lookup"><span data-stu-id="0d710-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="0d710-171">Да, поддерживается, что положительно сказывается на балансировке трафика в других виртуальных сетях.</span><span class="sxs-lookup"><span data-stu-id="0d710-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="0d710-172">**В. Давайте обсудим tooon локальные серверы при подключении по ExpressRoute или VPN-туннели?**</span><span class="sxs-lookup"><span data-stu-id="0d710-172">**Q. Can I talk tooon-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="0d710-173">Да, при условии, что разрешен трафик.</span><span class="sxs-lookup"><span data-stu-id="0d710-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="0d710-174">**В. Может ли один серверный пул обслуживать несколько приложений, используя разные порты?**</span><span class="sxs-lookup"><span data-stu-id="0d710-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="0d710-175">Поддерживается архитектура микрослужб.</span><span class="sxs-lookup"><span data-stu-id="0d710-175">Micro service architecture is supported.</span></span> <span data-ttu-id="0d710-176">Потребуется несколько tooprobe http параметры, настроенные на разные порты.</span><span class="sxs-lookup"><span data-stu-id="0d710-176">You would need multiple http settings configured tooprobe on different ports.</span></span>

<span data-ttu-id="0d710-177">**В. Поддерживают ли пользовательские пробы подстановочные знаки или регулярные выражения в данных ответа?**</span><span class="sxs-lookup"><span data-stu-id="0d710-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="0d710-178">Нет, не поддерживают.</span><span class="sxs-lookup"><span data-stu-id="0d710-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="0d710-179">**В. Как обрабатываются правила?**</span><span class="sxs-lookup"><span data-stu-id="0d710-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="0d710-180">Правила обрабатываются в порядке hello, в котором они настроены.</span><span class="sxs-lookup"><span data-stu-id="0d710-180">Rules are processed in hello order they are configured.</span></span> <span data-ttu-id="0d710-181">Рекомендуется, правила нескольких сайтов настроены перед основные правила tooreduce hello вероятность, что трафик будет направляться неуместные серверной toohello как hello базовое правило будет соответствовать трафик на основании правила для нескольких сайтов предыдущих toohello порта при вычислении.</span><span class="sxs-lookup"><span data-stu-id="0d710-181">It is recommended that multi-site rules are configured before basic rules tooreduce hello chance that traffic is routed toohello inappropriate backend as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="0d710-182">**В. Как обрабатываются правила?**</span><span class="sxs-lookup"><span data-stu-id="0d710-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="0d710-183">Правила обрабатываются в порядке hello, в котором они были созданы.</span><span class="sxs-lookup"><span data-stu-id="0d710-183">Rules are processed in hello order they are created.</span></span> <span data-ttu-id="0d710-184">Рекомендуется настроить правила для нескольких сайтов прежде, чем базовые правила.</span><span class="sxs-lookup"><span data-stu-id="0d710-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="0d710-185">Сначала настроить прослушиватели несколькими сайтами, это снижает вероятность hello, трафик является перенаправленное toohello неуместные серверной части.</span><span class="sxs-lookup"><span data-stu-id="0d710-185">By configuring multi-site listeners first, this configuration reduces hello chance that traffic is routed toohello inappropriate backend.</span></span> <span data-ttu-id="0d710-186">Эта проблема маршрутизации может происходить при hello базовое правило будет соответствовать трафик на основании правила для нескольких сайтов предыдущих toohello порта при вычислении.</span><span class="sxs-lookup"><span data-stu-id="0d710-186">This routing issue can occur as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="0d710-187">**В. Что означают поля hello узла для пользовательских проб?**</span><span class="sxs-lookup"><span data-stu-id="0d710-187">**Q. What does hello Host field for custom probes signify?**</span></span>

<span data-ttu-id="0d710-188">Поле узла указывает hello имя toosend hello модуль проверки для.</span><span class="sxs-lookup"><span data-stu-id="0d710-188">Host field specifies hello name toosend hello probe to.</span></span> <span data-ttu-id="0d710-189">Применяется только в случае, когда в шлюзе приложений настроено многосайтовое подключение. В противном случае используется значение 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="0d710-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="0d710-190">Это значение отличается от имени узла виртуальной машины и имеет следующий формат: \<протокол\>://\<узел\>:\<порт\>\<путь\>.</span><span class="sxs-lookup"><span data-stu-id="0d710-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="0d710-191">**В. Можно ли tooa доступа шлюз приложений белого списка лишь немногие исходного IP-адресов?**</span><span class="sxs-lookup"><span data-stu-id="0d710-191">**Q. Can I whitelist Application Gateway access tooa few source IPs?**</span></span>

<span data-ttu-id="0d710-192">Это можно сделать с помощью групп безопасности сети в подсети шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="0d710-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="0d710-193">Hello следующие ограничения должны быть помещены в подсети hello в порядке приоритета hello в списке:</span><span class="sxs-lookup"><span data-stu-id="0d710-193">hello following restrictions should be put on hello subnet in hello listed order of priority:</span></span>

* <span data-ttu-id="0d710-194">Разрешить входящий трафик из исходного IP-адреса или диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="0d710-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="0d710-195">Разрешить входящие запросы от всех источников tooports 65503 65534 для [взаимодействие работоспособности внутренних](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="0d710-195">Allow incoming requests from all sources tooports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="0d710-196">Разрешить входящие зондов подсистемы балансировки нагрузки Azure (тег "AzureLoadBalancer") и входящий трафик виртуального (тег "VirtualNetwork") на hello [NSG](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="0d710-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on hello [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="0d710-197">Запретить весь другой входящий трафик с помощью правила, запрещающего любой трафик.</span><span class="sxs-lookup"><span data-stu-id="0d710-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="0d710-198">Разрешить исходящий трафик toohello Интернет для всех мест назначения.</span><span class="sxs-lookup"><span data-stu-id="0d710-198">Allow outbound traffic toohello internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="0d710-199">Производительность</span><span class="sxs-lookup"><span data-stu-id="0d710-199">Performance</span></span>

<span data-ttu-id="0d710-200">**В. Каким образом шлюз приложений поддерживает высокий уровень доступности и масштабируемость?**</span><span class="sxs-lookup"><span data-stu-id="0d710-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="0d710-201">Если развернуто два или больше экземпляров, шлюз приложений поддерживает сценарии обеспечения высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="0d710-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="0d710-202">Azure распределяет эти экземпляры tooensure домены обновления и отказоустойчивости, все экземпляры не приводит к ошибке в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="0d710-202">Azure distributes these instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="0d710-203">Шлюз приложений поддерживает масштабируемости, добавив несколько экземпляров hello одинаковой нагрузки hello tooshare шлюза.</span><span class="sxs-lookup"><span data-stu-id="0d710-203">Application Gateway supports scalability by adding multiple instances of hello same gateway tooshare hello load.</span></span>

<span data-ttu-id="0d710-204">**В. Как добиться сценария аварийного восстановления в центрах обработки данных с помощью шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="0d710-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="0d710-205">Клиенты могут использовать диспетчер трафика toodistribute трафик через несколько шлюзов приложения в разных центрах обработки данных.</span><span class="sxs-lookup"><span data-stu-id="0d710-205">Customers can use Traffic Manager toodistribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="0d710-206">**В. Поддерживается ли автоматическое масштабирование?**</span><span class="sxs-lookup"><span data-stu-id="0d710-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="0d710-207">Нет, показатель пропускную способность, можно использовать tooalert, но шлюз приложений при достижении порога.</span><span class="sxs-lookup"><span data-stu-id="0d710-207">No, but Application Gateway has a throughput metric that can be used tooalert you when a threshold is reached.</span></span> <span data-ttu-id="0d710-208">Вручную добавив экземпляры или изменение размера не перезапустить шлюз hello и не влияет на существующие трафика.</span><span class="sxs-lookup"><span data-stu-id="0d710-208">Manually adding instances or changing size does not restart hello gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="0d710-209">**В. Вызывает ли увеличение или уменьшение масштабирования, выполненное вручную, простой?**</span><span class="sxs-lookup"><span data-stu-id="0d710-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="0d710-210">Нет, не вызывает. Экземпляры распределяются по доменам сбоя и обновления.</span><span class="sxs-lookup"><span data-stu-id="0d710-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="0d710-211">**В. Можно изменить размер экземпляра из среднего toolarge без перебоев в работе?**</span><span class="sxs-lookup"><span data-stu-id="0d710-211">**Q. Can I change instance size from medium toolarge without disruption?**</span></span>

<span data-ttu-id="0d710-212">Да, Azure распределяет экземпляры по tooensure домены обновления и отказоустойчивости, все экземпляры не приводит к ошибке в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="0d710-212">Yes, Azure distributes instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="0d710-213">Приложение поддерживает шлюза, масштабирование, добавив несколько экземпляров hello одинаковой нагрузки hello tooshare шлюза.</span><span class="sxs-lookup"><span data-stu-id="0d710-213">Application Gateway supports scaling by adding multiple instances of hello same gateway tooshare hello load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="0d710-214">Настройка SSL</span><span class="sxs-lookup"><span data-stu-id="0d710-214">SSL Configuration</span></span>

<span data-ttu-id="0d710-215">**В. Какие сертификаты поддерживает шлюз приложений?**</span><span class="sxs-lookup"><span data-stu-id="0d710-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="0d710-216">Поддерживаются самозаверяющие сертификаты, сертификаты ЦС и групповые.</span><span class="sxs-lookup"><span data-stu-id="0d710-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="0d710-217">Сертификаты высокой надежности не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="0d710-217">EV certs are not supported.</span></span>

<span data-ttu-id="0d710-218">**В. Что такое hello текущего шифров шлюза приложений**</span><span class="sxs-lookup"><span data-stu-id="0d710-218">**Q. What are hello current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="0d710-219">Здесь представлены Hello hello текущего шифров шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0d710-219">hello following are hello current cipher suites supported by application gateway.</span></span> <span data-ttu-id="0d710-220">Посетите: [Настройка SSL версии политики и комплектов шифров в шлюзе приложения](application-gateway-configure-ssl-policy-powershell.md) toolearn как toocustomize параметры SSL.</span><span class="sxs-lookup"><span data-stu-id="0d710-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn how toocustomize SSL options.</span></span>

- <span data-ttu-id="0d710-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="0d710-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="0d710-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="0d710-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="0d710-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="0d710-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="0d710-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="0d710-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="0d710-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="0d710-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="0d710-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="0d710-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="0d710-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="0d710-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="0d710-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="0d710-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="0d710-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="0d710-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="0d710-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="0d710-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="0d710-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="0d710-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="0d710-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="0d710-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="0d710-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="0d710-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="0d710-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="0d710-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="0d710-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="0d710-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="0d710-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="0d710-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="0d710-247">**В. Шлюз приложений также поддерживает повторное шифрование трафика toohello серверной?**</span><span class="sxs-lookup"><span data-stu-id="0d710-247">**Q. Does Application Gateway also support re-encryption of traffic toohello backend?**</span></span>

<span data-ttu-id="0d710-248">Да, разгрузки SSL поддерживает использование шлюза приложений и end tooend SSL, повторно шифрует серверной toohello трафика hello.</span><span class="sxs-lookup"><span data-stu-id="0d710-248">Yes, Application Gateway supports SSL offload, and end tooend SSL, which re-encrypts hello traffic toohello backend.</span></span>

<span data-ttu-id="0d710-249">**В. Можно настроить версии протокола SSL toocontrol политики SSL?**</span><span class="sxs-lookup"><span data-stu-id="0d710-249">**Q. Can I configure SSL policy toocontrol SSL Protocol versions?**</span></span>

<span data-ttu-id="0d710-250">Да, можно настроить шлюз приложений toodeny TLS1.0, TLS1.1 и TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="0d710-250">Yes, you can configure Application Gateway toodeny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="0d710-251">Протоколы SSL версий 2.0 и 3.0 уже отключены по умолчанию, и их настройки нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="0d710-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="0d710-252">**В. Можно ли настроить комплекты шифров и порядок политик?**</span><span class="sxs-lookup"><span data-stu-id="0d710-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="0d710-253">Да, имеется возможность [настроить комплекты шифров](application-gateway-ssl-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0d710-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="0d710-254">При определении пользовательской политики, необходимо включить хотя бы один из следующих комплектов шифров hello.</span><span class="sxs-lookup"><span data-stu-id="0d710-254">When defining a custom policy, at least one of hello following cipher suites must be enabled.</span></span> <span data-ttu-id="0d710-255">Шлюз приложений использует управление серверной toofor SHA256.</span><span class="sxs-lookup"><span data-stu-id="0d710-255">Application gateway uses SHA256 toofor backend management.</span></span>

* <span data-ttu-id="0d710-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="0d710-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="0d710-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="0d710-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="0d710-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="0d710-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="0d710-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="0d710-262">**В. Какое количество SSL-сертификатов поддерживается?**</span><span class="sxs-lookup"><span data-stu-id="0d710-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="0d710-263">Копирование too20 SSL сертификаты поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="0d710-263">Up too20 SSL certificates are supported.</span></span>

<span data-ttu-id="0d710-264">**В. Сколько сертификатов проверки подлинности поддерживается для повторного шифрования внутренней службы?**</span><span class="sxs-lookup"><span data-stu-id="0d710-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="0d710-265">Копирование too10 сертификаты проверки подлинности поддерживаются по умолчанию 5.</span><span class="sxs-lookup"><span data-stu-id="0d710-265">Up too10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="0d710-266">**В. Интегрируется ли шлюз приложений с Azure Key Vault изначально?**</span><span class="sxs-lookup"><span data-stu-id="0d710-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="0d710-267">Нет, он не интегрируется с этим хранилищем.</span><span class="sxs-lookup"><span data-stu-id="0d710-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="0d710-268">Настройка брандмауэра веб-приложения (WAF)</span><span class="sxs-lookup"><span data-stu-id="0d710-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="0d710-269">**В. Hello WAF SKU предоставляют все функции hello с hello стандартном номере SKU?**</span><span class="sxs-lookup"><span data-stu-id="0d710-269">**Q. Does hello WAF SKU offer all hello features available with hello Standard SKU?**</span></span>

<span data-ttu-id="0d710-270">Да, WAF поддерживает все функции hello в стандартном номере SKU hello.</span><span class="sxs-lookup"><span data-stu-id="0d710-270">Yes, WAF supports all hello features in hello Standard SKU.</span></span>

<span data-ttu-id="0d710-271">**В. Что такое hello CRS версию, которую поддерживает использование шлюза приложений**</span><span class="sxs-lookup"><span data-stu-id="0d710-271">**Q. What is hello CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="0d710-272">Шлюз приложений поддерживает [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) и CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="0d710-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="0d710-273">**В. Как отслеживать WAF?**</span><span class="sxs-lookup"><span data-stu-id="0d710-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="0d710-274">WAF отслеживается с помощью журнала ведения диагностики. Дополнительные сведения см. в статье [Мониторинг работоспособности серверной части, ведение журнала диагностики и метрики для шлюза приложений](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="0d710-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="0d710-275">**В. Блокирует ли трафик режим обнаружения?**</span><span class="sxs-lookup"><span data-stu-id="0d710-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="0d710-276">Нет, режим обнаружения только регистрирует трафик, активирующий правило WAF.</span><span class="sxs-lookup"><span data-stu-id="0d710-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="0d710-277">**В. Как настроить правила WAF?**</span><span class="sxs-lookup"><span data-stu-id="0d710-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="0d710-278">Да, WAF правила являются настраиваемыми, Дополнительные сведения о том, как toocustomize их посетите [WAF настроить группы правил и правила](application-gateway-customize-waf-rules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0d710-278">Yes, WAF rules are customizable, for more information on how toocustomize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="0d710-279">**В. Какие правила на сегодняшний день доступны?**</span><span class="sxs-lookup"><span data-stu-id="0d710-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="0d710-280">WAF в настоящее время поддерживает CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) и [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), предоставляющие базового плана безопасности по отношению к большинство hello первые 10 уязвимостей Привет открыть Web приложения безопасности проекта (OWASP) по следующему адресу [OWASP top 10 уязвимостей](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="0d710-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of hello top 10 vulnerabilities identified by hello Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="0d710-281">Защита от внедрения кода SQL.</span><span class="sxs-lookup"><span data-stu-id="0d710-281">SQL injection protection</span></span>

* <span data-ttu-id="0d710-282">Защита от межсайтовых сценариев.</span><span class="sxs-lookup"><span data-stu-id="0d710-282">Cross site scripting protection</span></span>

* <span data-ttu-id="0d710-283">Защита от распространенных сетевых атак, в том числе от внедрения команд, несанкционированных HTTP-запросов, разделения HTTP-запросов и атак с включением удаленного файла.</span><span class="sxs-lookup"><span data-stu-id="0d710-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="0d710-284">Защита от нарушений протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="0d710-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="0d710-285">Защита от аномалий протокола HTTP, например отсутствия агента пользователя узла и заголовков accept.</span><span class="sxs-lookup"><span data-stu-id="0d710-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="0d710-286">Защита от программ-роботов, программ-обходчиков и сканеров.</span><span class="sxs-lookup"><span data-stu-id="0d710-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="0d710-287">Обнаружение распространенных неправильных конфигураций приложений (Apache, IIS и т. д.).</span><span class="sxs-lookup"><span data-stu-id="0d710-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="0d710-288">**В. Поддерживает ли WAF также защиту от атак DDoS?**</span><span class="sxs-lookup"><span data-stu-id="0d710-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="0d710-289">Нет, не поддерживает.</span><span class="sxs-lookup"><span data-stu-id="0d710-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="0d710-290">Диагностика и ведение журнала</span><span class="sxs-lookup"><span data-stu-id="0d710-290">Diagnostics and Logging</span></span>

<span data-ttu-id="0d710-291">**В. Какие типы журналов доступны для шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="0d710-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="0d710-292">Для шлюза приложений доступны три журнала.</span><span class="sxs-lookup"><span data-stu-id="0d710-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="0d710-293">Дополнительные сведения о журналах и других диагностических возможностях см. в статье [Мониторинг работоспособности серверной части, ведение журнала диагностики и метрики для шлюза приложений](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="0d710-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="0d710-294">**ApplicationGatewayAccessLog** -журнал доступа hello содержит каждый запрос, переданный переднего плана toohello шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0d710-294">**ApplicationGatewayAccessLog** - hello access log contains each request submitted toohello Application Gateway frontend.</span></span> <span data-ttu-id="0d710-295">Hello данные включают hello вызывающего IP-адрес, URL-адрес запроса задержки ответа, возвращаемый код байт и выхода из системы. Данные для журнала доступа собираются каждые 300 секунд.</span><span class="sxs-lookup"><span data-stu-id="0d710-295">hello data includes hello caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="0d710-296">Этот журнал содержит одну запись для каждого экземпляра шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="0d710-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="0d710-297">**ApplicationGatewayPerformanceLog** -журнал производительности hello записывает сведения о производительности для каждого экземпляра всего запроса обслуживания, включая пропускную способность в байтах, обслуживаемых общее количество запросов, количество неудачных запросов, рабочих и нерабочих количество экземпляров серверной части.</span><span class="sxs-lookup"><span data-stu-id="0d710-297">**ApplicationGatewayPerformanceLog** - hello performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="0d710-298">**ApplicationGatewayFirewallLog** -журнала брандмауэра hello содержит запросы, которые регистрируются через режим обнаружения или Предотвращение шлюза приложения, настроенного с брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0d710-298">**ApplicationGatewayFirewallLog** - hello firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="0d710-299">**В. Как узнать, работоспособны ли участники серверного пула?**</span><span class="sxs-lookup"><span data-stu-id="0d710-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="0d710-300">Можно использовать командлет PowerShell hello `Get-AzureRmApplicationGatewayBackendHealth` или проверить работоспособность через портал hello, посетив [диагностики шлюза приложений](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="0d710-300">You can use hello PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through hello portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="0d710-301">**В. Что такое hello политики хранения журналов диагностики hello**</span><span class="sxs-lookup"><span data-stu-id="0d710-301">**Q. What is hello retention policy on hello diagnostics logs?**</span></span>

<span data-ttu-id="0d710-302">Журналы диагностики учетной записи хранения потока toohello клиентов и клиентов можно задать политику хранения hello, на основе их установки.</span><span class="sxs-lookup"><span data-stu-id="0d710-302">Diagnostic logs flow toohello customers storage account and customers can set hello retention policy based on their preference.</span></span> <span data-ttu-id="0d710-303">Также можно отправить журналы диагностики tooan концентратора событий или анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="0d710-303">Diagnostic logs can also be sent tooan Event Hub or Log Analytics.</span></span> <span data-ttu-id="0d710-304">Дополнительные сведения см. в статье [Мониторинг работоспособности серверной части, ведение журнала диагностики и метрики для шлюза приложений](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="0d710-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="0d710-305">**В. Как получить журналы аудита для шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="0d710-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="0d710-306">Для шлюза приложений доступны журналы аудита.</span><span class="sxs-lookup"><span data-stu-id="0d710-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="0d710-307">На портале hello щелкните **журнал действий** в колонке hello меню журнала аудита hello tooaccess шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="0d710-307">In hello portal, click **Activity Log** in hello menu blade of an Application Gateway tooaccess hello audit log.</span></span> 

<span data-ttu-id="0d710-308">**В. Можно ли настроить оповещения с помощью шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="0d710-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="0d710-309">Да, шлюз приложений поддерживает оповещения, которые настраиваются на основе метрик.</span><span class="sxs-lookup"><span data-stu-id="0d710-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="0d710-310">Шлюз приложений в настоящее время имеет показатель «пропускной способности», которая может быть настроенный tooalert.</span><span class="sxs-lookup"><span data-stu-id="0d710-310">Application Gateway currently has a metric of "throughput", which can be configured tooalert.</span></span> <span data-ttu-id="0d710-311">Посетите toolearn более о предупреждениях, [получать уведомления об оповещениях](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0d710-311">toolearn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="0d710-312">**В. Запрос работоспособности серверной части возвращает неизвестное состояние. Чем это может быть вызвано?**</span><span class="sxs-lookup"><span data-stu-id="0d710-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="0d710-313">Hello наиболее распространенной причиной является серверной toohello доступ заблокирован NSG или пользовательского DNS.</span><span class="sxs-lookup"><span data-stu-id="0d710-313">hello most common reason is access toohello backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="0d710-314">Посетите [серверной работоспособности, ведение журнала диагностики и метрики для шлюза приложения](application-gateway-diagnostics.md) toolearn дополнительные.</span><span class="sxs-lookup"><span data-stu-id="0d710-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d710-315">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0d710-315">Next Steps</span></span>

<span data-ttu-id="0d710-316">toolearn больше о шлюзе приложения посетите [tooApplication введение шлюза](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0d710-316">toolearn more about Application Gateway visit [Introduction tooApplication Gateway](application-gateway-introduction.md).</span></span>
