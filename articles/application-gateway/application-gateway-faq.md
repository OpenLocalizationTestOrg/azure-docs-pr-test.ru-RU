---
title: "Часто задаваемые вопросы о шлюзе приложений Azure | Документация Майкрософт"
description: "На этой странице содержатся ответы на часто задаваемые вопросы о шлюзе приложений Azure"
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
ms.openlocfilehash: 4e6244d92f41e0aa5c8a70db0db2881036984247
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="adc9e-103">Часто задаваемые вопросы о шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="adc9e-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="adc9e-104">Общие сведения</span><span class="sxs-lookup"><span data-stu-id="adc9e-104">General</span></span>

<span data-ttu-id="adc9e-105">**В. Что такое шлюз приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="adc9e-106">Шлюз приложений Azure является контроллером доставки приложений (ADC) как услуг, предлагающих для приложений разные функции балансировки нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="adc9e-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="adc9e-107">Это высокодоступная и масштабируемая служба, которая полностью управляется Azure.</span><span class="sxs-lookup"><span data-stu-id="adc9e-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="adc9e-108">**В. Какие функции поддерживает шлюз приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="adc9e-109">Шлюз приложений поддерживает разгрузку SSL и сквозной режим связи SSL, брандмауэр веб-приложения, сопоставление сеансов на основе файлов cookie, маршрутизацию на основе URL-пути, размещение нескольких сайтов и другие функции.</span><span class="sxs-lookup"><span data-stu-id="adc9e-109">Application Gateway supports SSL offloading and end to end SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="adc9e-110">Полный список поддерживаемых функций см. в статье [Обзор шлюза приложений](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-110">For a full list of supported features, visit [Introduction to Application Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="adc9e-111">**В. Какова разница между шлюзом приложений и Azure Load Balancer?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-111">**Q. What is the difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="adc9e-112">Шлюз приложений — балансировщик нагрузки уровня 7. Это означает, что он работает только с веб-трафиком (HTTP, HTTPS и WebSocket).</span><span class="sxs-lookup"><span data-stu-id="adc9e-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="adc9e-113">Он поддерживает такие функции, как завершение SSL-подключений, сопоставление сеансов на основе файлов cookie и циклический перебор для распределения нагрузки трафика.</span><span class="sxs-lookup"><span data-stu-id="adc9e-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="adc9e-114">С балансировщиком нагрузки доступна балансировка трафика уровня 4 (протоколы TCP и UDP).</span><span class="sxs-lookup"><span data-stu-id="adc9e-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="adc9e-115">**В. Какие протоколы поддерживает шлюз приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="adc9e-116">Шлюз приложений поддерживает протоколы HTTP, HTTPS и WebSocket.</span><span class="sxs-lookup"><span data-stu-id="adc9e-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="adc9e-117">**В. Какие ресурсы в настоящее время поддерживаются как часть серверного пула?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="adc9e-118">Внутренние пулы могут состоять из сетевых адаптеров, масштабируемых наборов виртуальных машин, общедоступных IP-адресов, внутренних IP-адресов, полных доменных имен и таких мультитенантых серверных частей, как веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="adc9e-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="adc9e-119">Участники серверного пула шлюза приложений не привязаны к группе доступности.</span><span class="sxs-lookup"><span data-stu-id="adc9e-119">Application Gateway backend pool members are not tied to an availability set.</span></span> <span data-ttu-id="adc9e-120">Они могут располагаться в кластерах, центрах обработки данных или за пределами портала Azure, пока у них есть возможность подключения по IP.</span><span class="sxs-lookup"><span data-stu-id="adc9e-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="adc9e-121">**В. В каких регионах доступна служба?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-121">**Q. What regions is the service available in?**</span></span>

<span data-ttu-id="adc9e-122">Шлюз приложений доступен во всех регионах глобальной платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="adc9e-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="adc9e-123">Он также доступен в [Azure для Китая](https://www.azure.cn/) и [Azure для государственных организаций](https://azure.microsoft.com/en-us/overview/clouds/government/).</span><span class="sxs-lookup"><span data-stu-id="adc9e-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="adc9e-124">**В. Это специальное развертывание для подписки или общее для всех клиентов?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="adc9e-125">Шлюз приложений — это специальное развертывание в вашей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="adc9e-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="adc9e-126">**В. Поддерживается ли перенаправление протоколов HTTP -> HTTPS?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="adc9e-127">Перенаправление поддерживается.</span><span class="sxs-lookup"><span data-stu-id="adc9e-127">Redirection is supported.</span></span> <span data-ttu-id="adc9e-128">Дополнительные сведения см. в статье [Общие сведения о перенаправлении для шлюза приложений](application-gateway-redirect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) to learn more.</span></span>

<span data-ttu-id="adc9e-129">**В. В каком порядке обрабатываются прослушиватели?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="adc9e-130">Прослушиватели обрабатываются в том порядке, в котором они указаны.</span><span class="sxs-lookup"><span data-stu-id="adc9e-130">Listeners are processed in the order they are shown.</span></span> <span data-ttu-id="adc9e-131">Поэтому если основной прослушиватель соответствует поступившему запросу, он обработает этот запрос первым.</span><span class="sxs-lookup"><span data-stu-id="adc9e-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="adc9e-132">Чтобы обеспечить маршрутизацию трафика в соответствующую внутреннюю службу, многосайтовые прослушиватели следует настроить до основного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="adc9e-132">Multi-site listeners should be configured before a basic listener to ensure traffic is routed to the correct back-end.</span></span>

<span data-ttu-id="adc9e-133">**В. Где найти IP-адрес и DNS-имя шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="adc9e-134">При использовании общедоступного IP-адреса в качестве конечной точки эти сведения вы можете найти в ресурсах общедоступного IP-адреса или на странице обзора для шлюза приложений на портале.</span><span class="sxs-lookup"><span data-stu-id="adc9e-134">When using a public IP address as an endpoint, this information can be found on the public IP address resource or on the Overview page for the Application Gateway in the portal.</span></span> <span data-ttu-id="adc9e-135">Для внутренних IP-адресов эту информацию можно найти на странице обзора.</span><span class="sxs-lookup"><span data-stu-id="adc9e-135">For internal IP addresses, this can be found on the Overview page.</span></span>

<span data-ttu-id="adc9e-136">**В. Меняются ли IP-адрес и DNS-имя в течение времени существования шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-136">**Q. Does the IP or DNS change over the lifetime of the Application Gateway?**</span></span>

<span data-ttu-id="adc9e-137">Виртуальный IP-адрес может измениться, если шлюз приложений остановлен и запущен клиентом.</span><span class="sxs-lookup"><span data-stu-id="adc9e-137">The VIP can change if the gateway is stopped and started by the customer.</span></span> <span data-ttu-id="adc9e-138">DNS-имя, связанное со шлюзом приложений, не меняется никогда.</span><span class="sxs-lookup"><span data-stu-id="adc9e-138">The DNS associated with Application Gateway does not change over the lifecycle of the gateway.</span></span> <span data-ttu-id="adc9e-139">По этой причине мы рекомендуем использовать псевдоним CNAME и настроить его для DNS-адреса шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="adc9e-139">For this reason, it is recommended to use a CNAME alias and point it to the DNS address of the Application Gateway.</span></span>

<span data-ttu-id="adc9e-140">**В. Поддерживает ли шлюз приложений статические IP-адреса?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="adc9e-141">Нет, шлюз приложений не поддерживает статические общедоступные IP-адреса, но поддерживает статические внутренние.</span><span class="sxs-lookup"><span data-stu-id="adc9e-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="adc9e-142">**В. Поддерживает ли шлюз приложений несколько общедоступных IP-адресов в шлюзе?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-142">**Q. Does Application Gateway support multiple public IPs on the gateway?**</span></span>

<span data-ttu-id="adc9e-143">Шлюз приложений поддерживает только один общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="adc9e-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="adc9e-144">**В. Поддерживает ли шлюз приложений заголовки X-Forwarded-For?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="adc9e-145">Да, шлюз приложений поддерживает заголовки X-Forwarded-For, X-Forwarded-Proto и X-Forwarded-Port в запросах, направленных к внутренней службе.</span><span class="sxs-lookup"><span data-stu-id="adc9e-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into the request forwarded to the backend.</span></span> <span data-ttu-id="adc9e-146">Формат заголовка X-Forwarded-For представляет собой разделенный запятыми список вида "IP-адрес:порт".</span><span class="sxs-lookup"><span data-stu-id="adc9e-146">The format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="adc9e-147">Допустимые значения для заголовка X-Forwarded-Proto — HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="adc9e-147">The valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="adc9e-148">Заголовок X-Forwarded-Port указывает порт, в котором запрос достигает шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="adc9e-148">X-forwarded-port specifies the port at which the request reached at the Application Gateway.</span></span>

<span data-ttu-id="adc9e-149">**В. Сколько времени требуется для развертывания шлюза приложений? Работает ли шлюз приложений во время обновления?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-149">**Q. How long does it take to deploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="adc9e-150">Подготовка новых развертываний шлюза приложений может занять до 20 минут.</span><span class="sxs-lookup"><span data-stu-id="adc9e-150">New Application Gateway deployments can take up to 20 minutes to provision.</span></span> <span data-ttu-id="adc9e-151">Изменения в размере или числе экземпляров не нарушают работу шлюза приложений, он остается активным во время обновления.</span><span class="sxs-lookup"><span data-stu-id="adc9e-151">Changes to instance size/count are not disruptive, and the gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="adc9e-152">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="adc9e-152">Configuration</span></span>

<span data-ttu-id="adc9e-153">**В. Всегда ли шлюз приложений развертывается в виртуальной сети?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="adc9e-154">Да, шлюз приложений всегда развертывается в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="adc9e-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="adc9e-155">Эта подсеть может содержать только шлюзы приложений.</span><span class="sxs-lookup"><span data-stu-id="adc9e-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="adc9e-156">**В. Может ли шлюз приложений взаимодействовать с экземплярами за пределами виртуальной сети?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-156">**Q. Can Application Gateway talk to instances outside its virtual network?**</span></span>

<span data-ttu-id="adc9e-157">Шлюз приложений может взаимодействовать с экземплярами за пределами виртуальной сети, к которой он относится, при наличии подключения по IP.</span><span class="sxs-lookup"><span data-stu-id="adc9e-157">Application Gateway can talk to instances outside of the virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="adc9e-158">Если вы планируете использовать внутренние IP-адреса в качестве участников серверного пула, потребуется [пиринговая связь между виртуальными сетями](../virtual-network/virtual-network-peering-overview.md) или [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-158">If you plan to use internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="adc9e-159">**В. Можно ли еще что-нибудь развернуть в подсети шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-159">**Q. Can I deploy anything else in the Application Gateway subnet?**</span></span>

<span data-ttu-id="adc9e-160">Нет, но вы можете развернуть другие шлюзы приложений в подсети.</span><span class="sxs-lookup"><span data-stu-id="adc9e-160">No, but you can deploy other application gateways in the subnet.</span></span>

<span data-ttu-id="adc9e-161">**В. Поддерживаются ли группы безопасности сети в подсети шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-161">**Q. Are Network Security Groups supported on the Application Gateway subnet?**</span></span>

<span data-ttu-id="adc9e-162">Группы безопасности сети поддерживаются подсетью шлюза приложений со следующими ограничениями:</span><span class="sxs-lookup"><span data-stu-id="adc9e-162">Network Security Groups are supported on the Application Gateway subnet with the following restrictions:</span></span>

* <span data-ttu-id="adc9e-163">Для портов 65503–65534 должны быть размещены исключения, чтобы внутренние службы работали правильно.</span><span class="sxs-lookup"><span data-stu-id="adc9e-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health to work correctly.</span></span>

* <span data-ttu-id="adc9e-164">Исходящее подключение к Интернету не может быть заблокировано.</span><span class="sxs-lookup"><span data-stu-id="adc9e-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="adc9e-165">Трафик из тега AzureLoadBalancer должен быть разрешен.</span><span class="sxs-lookup"><span data-stu-id="adc9e-165">Traffic from the AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="adc9e-166">**В. Какие у шлюза приложений ограничения? Можно ли увеличить эти ограничения?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-166">**Q. What are the limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="adc9e-167">Сведения об ограничениях см. в разделе [Ограничения шлюза приложений](../azure-subscription-service-limits.md#application-gateway-limits).</span><span class="sxs-lookup"><span data-stu-id="adc9e-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) to view the limits.</span></span>

<span data-ttu-id="adc9e-168">**В. Можно ли использовать шлюз приложений одновременно для внешнего и внутреннего трафика?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="adc9e-169">Да, каждый шлюз приложений может иметь один внутренний IP-адрес и один внешний.</span><span class="sxs-lookup"><span data-stu-id="adc9e-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="adc9e-170">**В. Поддерживается ли пиринговая связь между виртуальными сетями?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="adc9e-171">Да, поддерживается, что положительно сказывается на балансировке трафика в других виртуальных сетях.</span><span class="sxs-lookup"><span data-stu-id="adc9e-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="adc9e-172">**В. Можно ли взаимодействовать с локальными серверами, если они подключены через туннели ExpressRoute или VPN?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-172">**Q. Can I talk to on-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="adc9e-173">Да, при условии, что разрешен трафик.</span><span class="sxs-lookup"><span data-stu-id="adc9e-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="adc9e-174">**В. Может ли один серверный пул обслуживать несколько приложений, используя разные порты?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="adc9e-175">Поддерживается архитектура микрослужб.</span><span class="sxs-lookup"><span data-stu-id="adc9e-175">Micro service architecture is supported.</span></span> <span data-ttu-id="adc9e-176">Вам потребуется настроить несколько параметров HTTP для проверки различных портов.</span><span class="sxs-lookup"><span data-stu-id="adc9e-176">You would need multiple http settings configured to probe on different ports.</span></span>

<span data-ttu-id="adc9e-177">**В. Поддерживают ли пользовательские пробы подстановочные знаки или регулярные выражения в данных ответа?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="adc9e-178">Нет, не поддерживают.</span><span class="sxs-lookup"><span data-stu-id="adc9e-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="adc9e-179">**В. Как обрабатываются правила?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="adc9e-180">Правила обрабатываются в том порядке, в котором они были настроены.</span><span class="sxs-lookup"><span data-stu-id="adc9e-180">Rules are processed in the order they are configured.</span></span> <span data-ttu-id="adc9e-181">Многосайтовые правила рекомендуется настраивать до основных правил, чтобы снизить вероятность маршрутизации трафика в неправильную внутреннюю службу, так как основное правило будет сопоставляться с трафиком в соответствии с портом до оценки многосайтового правила.</span><span class="sxs-lookup"><span data-stu-id="adc9e-181">It is recommended that multi-site rules are configured before basic rules to reduce the chance that traffic is routed to the inappropriate backend as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="adc9e-182">**В. Как обрабатываются правила?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="adc9e-183">Правила обрабатываются в порядке создания.</span><span class="sxs-lookup"><span data-stu-id="adc9e-183">Rules are processed in the order they are created.</span></span> <span data-ttu-id="adc9e-184">Рекомендуется настроить правила для нескольких сайтов прежде, чем базовые правила.</span><span class="sxs-lookup"><span data-stu-id="adc9e-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="adc9e-185">Если сначала настроить прослушиватели для нескольких сайтов, это снизит вероятность направления трафика к несоответствующей серверной части.</span><span class="sxs-lookup"><span data-stu-id="adc9e-185">By configuring multi-site listeners first, this configuration reduces the chance that traffic is routed to the inappropriate backend.</span></span> <span data-ttu-id="adc9e-186">Эта проблема маршрутизации может возникнуть, так как базовое правило будет сопоставлять трафик по порту прежде, чем будет применено правило для нескольких сайтов.</span><span class="sxs-lookup"><span data-stu-id="adc9e-186">This routing issue can occur as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="adc9e-187">**В. Что означает поле "Узел" для пользовательских проб?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-187">**Q. What does the Host field for custom probes signify?**</span></span>

<span data-ttu-id="adc9e-188">Это поле указывает имя узла, куда необходимо отправить пробу.</span><span class="sxs-lookup"><span data-stu-id="adc9e-188">Host field specifies the name to send the probe to.</span></span> <span data-ttu-id="adc9e-189">Применяется только в случае, когда в шлюзе приложений настроено многосайтовое подключение. В противном случае используется значение 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="adc9e-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="adc9e-190">Это значение отличается от имени узла виртуальной машины и имеет следующий формат: \<протокол\>://\<узел\>:\<порт\>\<путь\>.</span><span class="sxs-lookup"><span data-stu-id="adc9e-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="adc9e-191">**В. Можно ли добавить в список разрешений доступ шлюза приложений к нескольким исходным IP-адресам?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-191">**Q. Can I whitelist Application Gateway access to a few source IPs?**</span></span>

<span data-ttu-id="adc9e-192">Это можно сделать с помощью групп безопасности сети в подсети шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="adc9e-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="adc9e-193">Следующие ограничения должны быть установлены для подсети в указанном порядке приоритета:</span><span class="sxs-lookup"><span data-stu-id="adc9e-193">The following restrictions should be put on the subnet in the listed order of priority:</span></span>

* <span data-ttu-id="adc9e-194">Разрешить входящий трафик из исходного IP-адреса или диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="adc9e-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="adc9e-195">Разрешить входящие запросы от всех источников на порты 65503–65534 для [просмотра работоспособности серверной части ](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-195">Allow incoming requests from all sources to ports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="adc9e-196">Разрешить пробы Azure Load Balancer (тег AzureLoadBalancer) и входящего виртуального сетевого трафика (тег VirtualNetwork) в [группах безопасности сети](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on the [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="adc9e-197">Запретить весь другой входящий трафик с помощью правила, запрещающего любой трафик.</span><span class="sxs-lookup"><span data-stu-id="adc9e-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="adc9e-198">Разрешить исходящий трафик в Интернет для всех назначений.</span><span class="sxs-lookup"><span data-stu-id="adc9e-198">Allow outbound traffic to the internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="adc9e-199">Производительность</span><span class="sxs-lookup"><span data-stu-id="adc9e-199">Performance</span></span>

<span data-ttu-id="adc9e-200">**В. Каким образом шлюз приложений поддерживает высокий уровень доступности и масштабируемость?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="adc9e-201">Если развернуто два или больше экземпляров, шлюз приложений поддерживает сценарии обеспечения высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="adc9e-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="adc9e-202">Azure распределяет эти экземпляры по доменам сбоя и обновления, чтобы гарантировать, что все экземпляры не завершатся ошибкой в одно и то же время.</span><span class="sxs-lookup"><span data-stu-id="adc9e-202">Azure distributes these instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="adc9e-203">Шлюз приложений поддерживает масштабируемость путем добавления нескольких экземпляров одного шлюза для распределения нагрузки.</span><span class="sxs-lookup"><span data-stu-id="adc9e-203">Application Gateway supports scalability by adding multiple instances of the same gateway to share the load.</span></span>

<span data-ttu-id="adc9e-204">**В. Как добиться сценария аварийного восстановления в центрах обработки данных с помощью шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="adc9e-205">Клиенты могут использовать диспетчер трафика для распределения трафика между несколькими шлюзами приложений в разных центрах обработки данных.</span><span class="sxs-lookup"><span data-stu-id="adc9e-205">Customers can use Traffic Manager to distribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="adc9e-206">**В. Поддерживается ли автоматическое масштабирование?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="adc9e-207">Нет, не поддерживается, но есть метрика пропускной способности, используемая для оповещений при достижении порогового значения.</span><span class="sxs-lookup"><span data-stu-id="adc9e-207">No, but Application Gateway has a throughput metric that can be used to alert you when a threshold is reached.</span></span> <span data-ttu-id="adc9e-208">При добавлении экземпляров или изменении размеров вручную шлюз не перезапускается, и это не влияет на существующий трафик.</span><span class="sxs-lookup"><span data-stu-id="adc9e-208">Manually adding instances or changing size does not restart the gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="adc9e-209">**В. Вызывает ли увеличение или уменьшение масштабирования, выполненное вручную, простой?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="adc9e-210">Нет, не вызывает. Экземпляры распределяются по доменам сбоя и обновления.</span><span class="sxs-lookup"><span data-stu-id="adc9e-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="adc9e-211">**В. Можно ли изменить размер экземпляра со среднего на большой без прерывания?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-211">**Q. Can I change instance size from medium to large without disruption?**</span></span>

<span data-ttu-id="adc9e-212">Да, можно. Azure распределяет экземпляры по доменам сбоя и обновления, чтобы гарантировать, что все экземпляры не завершатся ошибкой в одно и то же время.</span><span class="sxs-lookup"><span data-stu-id="adc9e-212">Yes, Azure distributes instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="adc9e-213">Шлюз приложений поддерживает масштабирование путем добавления нескольких экземпляров одного шлюза для распределения нагрузки.</span><span class="sxs-lookup"><span data-stu-id="adc9e-213">Application Gateway supports scaling by adding multiple instances of the same gateway to share the load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="adc9e-214">Настройка SSL</span><span class="sxs-lookup"><span data-stu-id="adc9e-214">SSL Configuration</span></span>

<span data-ttu-id="adc9e-215">**В. Какие сертификаты поддерживает шлюз приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="adc9e-216">Поддерживаются самозаверяющие сертификаты, сертификаты ЦС и групповые.</span><span class="sxs-lookup"><span data-stu-id="adc9e-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="adc9e-217">Сертификаты высокой надежности не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="adc9e-217">EV certs are not supported.</span></span>

<span data-ttu-id="adc9e-218">**В. Какие текущие комплекты шифров поддерживает шлюз приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-218">**Q. What are the current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="adc9e-219">Ниже представлены текущие комплекты шифров, поддерживаемые шлюзом приложений.</span><span class="sxs-lookup"><span data-stu-id="adc9e-219">The following are the current cipher suites supported by application gateway.</span></span> <span data-ttu-id="adc9e-220">Дополнительные сведения о настройке параметров SSL см. в статье [Настройка версий политики SSL и комплектов шифров на шлюзе приложений](application-gateway-configure-ssl-policy-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn how to customize SSL options.</span></span>

- <span data-ttu-id="adc9e-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="adc9e-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="adc9e-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="adc9e-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="adc9e-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="adc9e-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="adc9e-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="adc9e-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="adc9e-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="adc9e-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="adc9e-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="adc9e-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="adc9e-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="adc9e-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="adc9e-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="adc9e-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="adc9e-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="adc9e-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="adc9e-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="adc9e-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="adc9e-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="adc9e-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="adc9e-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="adc9e-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="adc9e-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="adc9e-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="adc9e-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="adc9e-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="adc9e-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="adc9e-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="adc9e-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="adc9e-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="adc9e-247">**В. Поддерживает ли также шлюз приложений повторное шифрование трафика к внутренней службе?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-247">**Q. Does Application Gateway also support re-encryption of traffic to the backend?**</span></span>

<span data-ttu-id="adc9e-248">Да, шлюз поддерживает разгрузку SSL и сквозной режим связи SSL, повторно шифрующие трафик к внутренней службе.</span><span class="sxs-lookup"><span data-stu-id="adc9e-248">Yes, Application Gateway supports SSL offload, and end to end SSL, which re-encrypts the traffic to the backend.</span></span>

<span data-ttu-id="adc9e-249">**В. Можно ли настроить политику SSL для контроля версий протокола SSL?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-249">**Q. Can I configure SSL policy to control SSL Protocol versions?**</span></span>

<span data-ttu-id="adc9e-250">Да, вы можете настроить шлюз приложений, чтобы запретить версии TLS 1.0, TLS 1.1 и TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="adc9e-250">Yes, you can configure Application Gateway to deny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="adc9e-251">Протоколы SSL версий 2.0 и 3.0 уже отключены по умолчанию, и их настройки нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="adc9e-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="adc9e-252">**В. Можно ли настроить комплекты шифров и порядок политик?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="adc9e-253">Да, имеется возможность [настроить комплекты шифров](application-gateway-ssl-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="adc9e-254">При определении пользовательской политики необходимо включить хотя бы один из следующих комплектов шифров.</span><span class="sxs-lookup"><span data-stu-id="adc9e-254">When defining a custom policy, at least one of the following cipher suites must be enabled.</span></span> <span data-ttu-id="adc9e-255">Шлюз приложений использует SHA256 для управления серверной частью.</span><span class="sxs-lookup"><span data-stu-id="adc9e-255">Application gateway uses SHA256 to for backend management.</span></span>

* <span data-ttu-id="adc9e-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="adc9e-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="adc9e-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="adc9e-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="adc9e-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="adc9e-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="adc9e-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="adc9e-262">**В. Какое количество SSL-сертификатов поддерживается?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="adc9e-263">Поддерживается до 20 сертификатов.</span><span class="sxs-lookup"><span data-stu-id="adc9e-263">Up to 20 SSL certificates are supported.</span></span>

<span data-ttu-id="adc9e-264">**В. Сколько сертификатов проверки подлинности поддерживается для повторного шифрования внутренней службы?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="adc9e-265">Поддерживается до 10 сертификатов. По умолчанию — 5.</span><span class="sxs-lookup"><span data-stu-id="adc9e-265">Up to 10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="adc9e-266">**В. Интегрируется ли шлюз приложений с Azure Key Vault изначально?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="adc9e-267">Нет, он не интегрируется с этим хранилищем.</span><span class="sxs-lookup"><span data-stu-id="adc9e-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="adc9e-268">Настройка брандмауэра веб-приложения (WAF)</span><span class="sxs-lookup"><span data-stu-id="adc9e-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="adc9e-269">**В. Доступны ли функции SKU категории "Стандартный" в SKU WAF?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-269">**Q. Does the WAF SKU offer all the features available with the Standard SKU?**</span></span>

<span data-ttu-id="adc9e-270">Да, доступны.</span><span class="sxs-lookup"><span data-stu-id="adc9e-270">Yes, WAF supports all the features in the Standard SKU.</span></span>

<span data-ttu-id="adc9e-271">**В. Какую версию CRS поддерживает шлюз приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-271">**Q. What is the CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="adc9e-272">Шлюз приложений поддерживает [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) и CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="adc9e-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="adc9e-273">**В. Как отслеживать WAF?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="adc9e-274">WAF отслеживается с помощью журнала ведения диагностики. Дополнительные сведения см. в статье [Мониторинг работоспособности серверной части, ведение журнала диагностики и метрики для шлюза приложений](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="adc9e-275">**В. Блокирует ли трафик режим обнаружения?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="adc9e-276">Нет, режим обнаружения только регистрирует трафик, активирующий правило WAF.</span><span class="sxs-lookup"><span data-stu-id="adc9e-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="adc9e-277">**В. Как настроить правила WAF?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="adc9e-278">Да, правила WAF можно настраивать. Дополнительные сведения об этом см. в статье [Настройка правил брандмауэра веб-приложения на портале](application-gateway-customize-waf-rules-portal.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-278">Yes, WAF rules are customizable, for more information on how to customize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="adc9e-279">**В. Какие правила на сегодняшний день доступны?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="adc9e-280">В настоящее время WAF поддерживает CRS версий [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) и [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), что обеспечивает базовую защиту от наиболее важных уязвимостей, определенных открытым проектом безопасности веб-приложений (OWASP). Список 10 распространенных уязвимостей доступен [здесь](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013).</span><span class="sxs-lookup"><span data-stu-id="adc9e-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of the top 10 vulnerabilities identified by the Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="adc9e-281">Защита от внедрения кода SQL.</span><span class="sxs-lookup"><span data-stu-id="adc9e-281">SQL injection protection</span></span>

* <span data-ttu-id="adc9e-282">Защита от межсайтовых сценариев.</span><span class="sxs-lookup"><span data-stu-id="adc9e-282">Cross site scripting protection</span></span>

* <span data-ttu-id="adc9e-283">Защита от распространенных сетевых атак, в том числе от внедрения команд, несанкционированных HTTP-запросов, разделения HTTP-запросов и атак с включением удаленного файла.</span><span class="sxs-lookup"><span data-stu-id="adc9e-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="adc9e-284">Защита от нарушений протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="adc9e-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="adc9e-285">Защита от аномалий протокола HTTP, например отсутствия агента пользователя узла и заголовков accept.</span><span class="sxs-lookup"><span data-stu-id="adc9e-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="adc9e-286">Защита от программ-роботов, программ-обходчиков и сканеров.</span><span class="sxs-lookup"><span data-stu-id="adc9e-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="adc9e-287">Обнаружение распространенных неправильных конфигураций приложений (Apache, IIS и т. д.).</span><span class="sxs-lookup"><span data-stu-id="adc9e-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="adc9e-288">**В. Поддерживает ли WAF также защиту от атак DDoS?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="adc9e-289">Нет, не поддерживает.</span><span class="sxs-lookup"><span data-stu-id="adc9e-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="adc9e-290">Диагностика и ведение журнала</span><span class="sxs-lookup"><span data-stu-id="adc9e-290">Diagnostics and Logging</span></span>

<span data-ttu-id="adc9e-291">**В. Какие типы журналов доступны для шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="adc9e-292">Для шлюза приложений доступны три журнала.</span><span class="sxs-lookup"><span data-stu-id="adc9e-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="adc9e-293">Дополнительные сведения о журналах и других диагностических возможностях см. в статье [Мониторинг работоспособности серверной части, ведение журнала диагностики и метрики для шлюза приложений](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="adc9e-294">**ApplicationGatewayAccessLog**. В журнале доступа содержится каждый запрос, переданный во внешний интерфейс шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="adc9e-294">**ApplicationGatewayAccessLog** - The access log contains each request submitted to the Application Gateway frontend.</span></span> <span data-ttu-id="adc9e-295">Здесь указаны такие данные, как IP-адрес вызывающего объекта, запрашиваемый URL-адрес, задержка ответа, код возврата, входящие и исходящие байты. Данные для журнала доступа собираются каждые 300 секунд.</span><span class="sxs-lookup"><span data-stu-id="adc9e-295">The data includes the caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="adc9e-296">Этот журнал содержит одну запись для каждого экземпляра шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="adc9e-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="adc9e-297">**ApplicationGatewayPerformanceLog**. В журнал производительности записываются сведения о производительности каждого экземпляра, включая общее число обработанных запросов, пропускную способность в байтах, число неудачных запросов, а также число работоспособных и неработоспособных серверных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="adc9e-297">**ApplicationGatewayPerformanceLog** - The performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="adc9e-298">**ApplicationGatewayFirewallLog**. Журнал брандмауэра содержит запросы, которые были зарегистрированы в режиме обнаружения или предотвращения на шлюзе приложений, на котором настроен брандмауэр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="adc9e-298">**ApplicationGatewayFirewallLog** - The firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="adc9e-299">**В. Как узнать, работоспособны ли участники серверного пула?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="adc9e-300">Вы можете использовать командлет PowerShell `Get-AzureRmApplicationGatewayBackendHealth` или проверить работоспособность через портал, ознакомившись со сведениями в статье [Мониторинг работоспособности серверной части, ведение журнала диагностики и метрики для шлюза приложений](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-300">You can use the PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through the portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="adc9e-301">**В. Что такое политика хранения журналов диагностики?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-301">**Q. What is the retention policy on the diagnostics logs?**</span></span>

<span data-ttu-id="adc9e-302">Журналы диагностики находятся в учетных записях хранения клиентов, и клиенты могут задать политику хранения в зависимости от своих предпочтений.</span><span class="sxs-lookup"><span data-stu-id="adc9e-302">Diagnostic logs flow to the customers storage account and customers can set the retention policy based on their preference.</span></span> <span data-ttu-id="adc9e-303">Журналы диагностики также можно отправить в концентратор событий или службу Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="adc9e-303">Diagnostic logs can also be sent to an Event Hub or Log Analytics.</span></span> <span data-ttu-id="adc9e-304">Дополнительные сведения см. в статье [Мониторинг работоспособности серверной части, ведение журнала диагностики и метрики для шлюза приложений](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="adc9e-305">**В. Как получить журналы аудита для шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="adc9e-306">Для шлюза приложений доступны журналы аудита.</span><span class="sxs-lookup"><span data-stu-id="adc9e-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="adc9e-307">Чтобы перейти к такому журналу, на портале в колонке меню шлюза приложений щелкните **Журнал действий**.</span><span class="sxs-lookup"><span data-stu-id="adc9e-307">In the portal, click **Activity Log** in the menu blade of an Application Gateway to access the audit log.</span></span> 

<span data-ttu-id="adc9e-308">**В. Можно ли настроить оповещения с помощью шлюза приложений?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="adc9e-309">Да, шлюз приложений поддерживает оповещения, которые настраиваются на основе метрик.</span><span class="sxs-lookup"><span data-stu-id="adc9e-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="adc9e-310">На сегодняшний день у шлюза приложений есть метрика пропускной способности, для которой можно настроить оповещения.</span><span class="sxs-lookup"><span data-stu-id="adc9e-310">Application Gateway currently has a metric of "throughput", which can be configured to alert.</span></span> <span data-ttu-id="adc9e-311">Дополнительные сведения об оповещениях см. в статье [Получение уведомлений об оповещениях](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-311">To learn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="adc9e-312">**В. Запрос работоспособности серверной части возвращает неизвестное состояние. Чем это может быть вызвано?**</span><span class="sxs-lookup"><span data-stu-id="adc9e-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="adc9e-313">Самая распространенная причина — доступ к внутренней службе заблокирован группой безопасности сети (NSG) или пользовательской службой DNS.</span><span class="sxs-lookup"><span data-stu-id="adc9e-313">The most common reason is access to the backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="adc9e-314">Дополнительные сведения см. в статье [Мониторинг работоспособности серверной части, ведение журнала диагностики и метрики для шлюза приложений](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adc9e-315">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="adc9e-315">Next Steps</span></span>

<span data-ttu-id="adc9e-316">Дополнительные сведения о шлюзе приложений см. в статье [Обзор шлюза приложений](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="adc9e-316">To learn more about Application Gateway visit [Introduction to Application Gateway](application-gateway-introduction.md).</span></span>
