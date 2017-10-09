---
title: "Планирование и проектирование распределенных подключений: VPN-шлюз Azure | Документация Майкрософт"
description: "Сведения о планировании и проектировании VPN-шлюза для подключений между организациями и между виртуальными сетями, а также гибридных подключений"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="4d864-103">Планирование и проектирование VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="4d864-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="4d864-104">Планирование и проектирование конфигураций распределенных подключений и подключений между виртуальными сетями может быть очень простым или достаточно сложным в зависимости от потребностей сети.</span><span class="sxs-lookup"><span data-stu-id="4d864-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="4d864-105">В этой статье рассматриваются основные вопросы планирования и проектирования.</span><span class="sxs-lookup"><span data-stu-id="4d864-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="4d864-106"><a name="planning"></a>Планирование</span><span class="sxs-lookup"><span data-stu-id="4d864-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="4d864-107"><a name="compare"></a>Возможности распределенного подключения</span><span class="sxs-lookup"><span data-stu-id="4d864-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="4d864-108">Если tooconnect локальных сайтов безопасно tooa виртуальной сети, поэтому имеется три toodo различными способами: сайт-сайт, точка-сеть и ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4d864-108">If you want tooconnect your on-premises sites securely tooa virtual network, you have three different ways toodo so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="4d864-109">Сравните доступных подключений hello различных между организациями.</span><span class="sxs-lookup"><span data-stu-id="4d864-109">Compare hello different cross-premises connections that are available.</span></span> <span data-ttu-id="4d864-110">параметр Hello могут зависеть от различные соображения, такие как:</span><span class="sxs-lookup"><span data-stu-id="4d864-110">hello option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="4d864-111">Какая пропускная способность требуется для решения?</span><span class="sxs-lookup"><span data-stu-id="4d864-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="4d864-112">Вы действительно toocommunicate через hello общедоступный Интернет через безопасное VPN или частного подключения?</span><span class="sxs-lookup"><span data-stu-id="4d864-112">Do you want toocommunicate over hello public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="4d864-113">У вас есть открытый IP адрес доступных toouse?</span><span class="sxs-lookup"><span data-stu-id="4d864-113">Do you have a public IP address available toouse?</span></span>
* <span data-ttu-id="4d864-114">Планируется ли toouse VPN-устройства?</span><span class="sxs-lookup"><span data-stu-id="4d864-114">Are you planning toouse a VPN device?</span></span> <span data-ttu-id="4d864-115">Если да, является ли оно совместимым?</span><span class="sxs-lookup"><span data-stu-id="4d864-115">If so, is it compatible?</span></span>
* <span data-ttu-id="4d864-116">Вы подключаете лишь несколько компьютеров или требуется постоянное подключения для сайта?</span><span class="sxs-lookup"><span data-stu-id="4d864-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="4d864-117">Какой тип VPN-шлюз необходим для hello решения требуется toocreate?</span><span class="sxs-lookup"><span data-stu-id="4d864-117">What type of VPN gateway is required for hello solution you want toocreate?</span></span>
* <span data-ttu-id="4d864-118">Какой номер SKU шлюза следует использовать?</span><span class="sxs-lookup"><span data-stu-id="4d864-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="4d864-119"><a name="planningtable"></a>Таблица планирования</span><span class="sxs-lookup"><span data-stu-id="4d864-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="4d864-120">в следующей таблице Hello поможет выбрать hello оптимальный тип подключения для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="4d864-120">hello following table can help you decide hello best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="4d864-121"><a name="gwsku"></a>SKU шлюзов</span><span class="sxs-lookup"><span data-stu-id="4d864-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="4d864-122"><a name="wf"></a>Рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="4d864-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="4d864-123">Hello следующий список содержит hello общий рабочий процесс для подключения к облачной:</span><span class="sxs-lookup"><span data-stu-id="4d864-123">hello following list outlines hello common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="4d864-124">Проектирование и план, что ваш адрес подключения к топологии и список hello пространства для всех сетей должны tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4d864-124">Design and plan your connectivity topology and list hello address spaces for all networks you want tooconnect.</span></span>
2. <span data-ttu-id="4d864-125">Создайте виртуальную сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="4d864-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="4d864-126">Создание VPN-шлюза для виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="4d864-126">Create a VPN gateway for hello virtual network.</span></span>
4. <span data-ttu-id="4d864-127">Создание и настройка подключения tooon локальные сети или другими виртуальными сетями (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="4d864-127">Create and configure connections tooon-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="4d864-128">Создайте и настройте подключение "точка — сеть" для VPN-шлюза Azure (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="4d864-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="4d864-129"><a name="design"></a>Проектирование</span><span class="sxs-lookup"><span data-stu-id="4d864-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="4d864-130"><a name="topologies"></a>Топологии подключений</span><span class="sxs-lookup"><span data-stu-id="4d864-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="4d864-131">Сначала рассматривается схемам hello в hello [о VPN-шлюз](vpn-gateway-about-vpngateways.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="4d864-131">Start by looking at hello diagrams in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="4d864-132">статья Hello содержит простых схем, hello модели развертывания для каждой топологии и hello доступных средств развертывания можно использовать toodeploy конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4d864-132">hello article contains basic diagrams, hello deployment models for each topology, and hello available deployment tools you can use toodeploy your configuration.</span></span>

### <span data-ttu-id="4d864-133"><a name="designbasics"></a>Основы проектирования</span><span class="sxs-lookup"><span data-stu-id="4d864-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="4d864-134">Привет, в следующих разделах рассматриваются основы шлюза VPN hello.</span><span class="sxs-lookup"><span data-stu-id="4d864-134">hello following sections discuss hello VPN gateway basics.</span></span> 

#### <span data-ttu-id="4d864-135"><a name="servicelimits"></a>Ограничения сетевых служб</span><span class="sxs-lookup"><span data-stu-id="4d864-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="4d864-136">Прокрутите hello таблицы tooview [сетевые службы ограничения](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="4d864-136">Scroll through hello tables tooview [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="4d864-137">в списке пределов Hello может повлиять на проект.</span><span class="sxs-lookup"><span data-stu-id="4d864-137">hello limits listed may impact your design.</span></span>

#### <span data-ttu-id="4d864-138"><a name="subnets"></a>О подсетях</span><span class="sxs-lookup"><span data-stu-id="4d864-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="4d864-139">При создании подключений необходимо определить диапазоны адресов подсетей.</span><span class="sxs-lookup"><span data-stu-id="4d864-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="4d864-140">Нельзя, чтобы они перекрывались.</span><span class="sxs-lookup"><span data-stu-id="4d864-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="4d864-141">Привет, содержащихся в одном адресном пространстве, hello другое местоположение содержит одно расположение виртуальной сети или локально при перекрывающейся подсетью.</span><span class="sxs-lookup"><span data-stu-id="4d864-141">An overlapping subnet is when one virtual network or on-premises location contains hello same address space that hello other location contains.</span></span> <span data-ttu-id="4d864-142">Это означает должны специалистов сети toocarve сети вашей локальной вне диапазона для вас toouse для Azure IP-адресации пространства и подсети.</span><span class="sxs-lookup"><span data-stu-id="4d864-142">This means that you need your network engineers for your local on-premises networks toocarve out a range for you toouse for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="4d864-143">Необходимо, чтобы адресное пространство, которое не используется в локальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="4d864-143">You need address space that is not being used on hello local on-premises network.</span></span>

<span data-ttu-id="4d864-144">Перекрытие подсетей также следует предотвратить при работе с подключениями между виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="4d864-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="4d864-145">Если перекрываются подсетей и IP-адрес существует в отправке hello и назначении виртуальных сетей, сбой подключения к виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="4d864-145">If your subnets overlap and an IP address exists in both hello sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="4d864-146">Azure не может направить toohello данных hello другой виртуальной сети так, как адрес назначения hello является частью hello отправки виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="4d864-146">Azure can't route hello data toohello other VNet because hello destination address is part of hello sending VNet.</span></span>

<span data-ttu-id="4d864-147">Для работы VPN-шлюзов требуется специальная подсеть, которая называется подсетью шлюза.</span><span class="sxs-lookup"><span data-stu-id="4d864-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="4d864-148">Все подсети шлюза должен иметь имя GatewaySubnet toowork должным образом.</span><span class="sxs-lookup"><span data-stu-id="4d864-148">All gateway subnets must be named GatewaySubnet toowork properly.</span></span> <span data-ttu-id="4d864-149">Убедитесь, что не tooname в другой подсети шлюза имя и не используется развертывание виртуальных машин и т.д подсеть шлюза toohello.</span><span class="sxs-lookup"><span data-stu-id="4d864-149">Be sure not tooname your gateway subnet a different name, and don't deploy VMs or anything else toohello gateway subnet.</span></span> <span data-ttu-id="4d864-150">Ознакомьтесь с [подсетями шлюза](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="4d864-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="4d864-151"><a name="local"></a>О локальных сетевых шлюзах</span><span class="sxs-lookup"><span data-stu-id="4d864-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="4d864-152">шлюз локальной сети Hello обычно относится tooyour в локальном расположении.</span><span class="sxs-lookup"><span data-stu-id="4d864-152">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="4d864-153">В hello классической модели развертывания шлюз локальной сети hello является ссылка tooas сайт локальной сети.</span><span class="sxs-lookup"><span data-stu-id="4d864-153">In hello classic deployment model, hello local network gateway is referred tooas a Local Network Site.</span></span> <span data-ttu-id="4d864-154">При настройке шлюза локальной сети, присвойте ему имя, укажите hello общедоступный IP-адрес VPN-устройство локальной hello и указывать префиксы адресов hello, расположенных в папках локальной hello.</span><span class="sxs-lookup"><span data-stu-id="4d864-154">When you configure a local network gateway, you give it a name, specify hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are in hello on-premises location.</span></span> <span data-ttu-id="4d864-155">Azure просматривает hello префиксов адресов конечного сетевого трафика, обращается hello конфигурации, который указан для шлюза локальной сети hello и соответствующим образом направляет пакеты.</span><span class="sxs-lookup"><span data-stu-id="4d864-155">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for hello local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="4d864-156">При необходимости можно изменить префиксы адресов hello.</span><span class="sxs-lookup"><span data-stu-id="4d864-156">You can modify hello address prefixes as needed.</span></span> <span data-ttu-id="4d864-157">Дополнительные сведения см. в статье [Шлюзы локальной сети](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="4d864-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="4d864-158"><a name="gwtype"></a>О типах шлюзов</span><span class="sxs-lookup"><span data-stu-id="4d864-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="4d864-159">Выбор типа шлюза правильный hello для используемой топологии важен.</span><span class="sxs-lookup"><span data-stu-id="4d864-159">Selecting hello correct gateway type for your topology is critical.</span></span> <span data-ttu-id="4d864-160">Если выбран неправильный тип hello, шлюз не будет работать должным образом.</span><span class="sxs-lookup"><span data-stu-id="4d864-160">If you select hello wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="4d864-161">Тип шлюза Hello указывает, как сам шлюз hello подключается и необходимый параметр конфигурации для модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="4d864-161">hello gateway type specifies how hello gateway itself connects and is a required configuration setting for hello Resource Manager deployment model.</span></span>

<span data-ttu-id="4d864-162">Ниже приведены типы Hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="4d864-162">hello gateway types are:</span></span>

* <span data-ttu-id="4d864-163">Vpn</span><span class="sxs-lookup"><span data-stu-id="4d864-163">Vpn</span></span>
* <span data-ttu-id="4d864-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4d864-164">ExpressRoute</span></span>

#### <span data-ttu-id="4d864-165"><a name="connectiontype"></a>О типах подключений</span><span class="sxs-lookup"><span data-stu-id="4d864-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="4d864-166">Для каждой конфигурации необходим конкретный тип подключения.</span><span class="sxs-lookup"><span data-stu-id="4d864-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="4d864-167">Ниже приведены типы подключения Hello.</span><span class="sxs-lookup"><span data-stu-id="4d864-167">hello connection types are:</span></span>

* <span data-ttu-id="4d864-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="4d864-168">IPsec</span></span>
* <span data-ttu-id="4d864-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="4d864-169">Vnet2Vnet</span></span>
* <span data-ttu-id="4d864-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4d864-170">ExpressRoute</span></span>
* <span data-ttu-id="4d864-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="4d864-171">VPNClient</span></span>

#### <span data-ttu-id="4d864-172"><a name="vpntype"></a>О типах VPN</span><span class="sxs-lookup"><span data-stu-id="4d864-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="4d864-173">Для каждой конфигурации нужен определенный тип VPN.</span><span class="sxs-lookup"><span data-stu-id="4d864-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="4d864-174">Если необходимо скомбинировать две конфигурации, таких как создание toohello подключение точка-сеть "и" сеть-сеть соединения одной виртуальной сети, необходимо использовать тип VPN, который удовлетворяет требованиям оба соединения.</span><span class="sxs-lookup"><span data-stu-id="4d864-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection toohello same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="4d864-175">Hello следующих таблицах показаны тип VPN hello как он был сопоставлен tooeach конфигурация подключения.</span><span class="sxs-lookup"><span data-stu-id="4d864-175">hello following tables show hello VPN type as it maps tooeach connection configuration.</span></span> <span data-ttu-id="4d864-176">Убедитесь, что hello тип VPN, которые должны toocreate hello конфигурации шлюза совпадений для.</span><span class="sxs-lookup"><span data-stu-id="4d864-176">Make sure hello VPN type for your gateway matches hello configuration that you want toocreate.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="4d864-177"><a name="devices"></a>VPN-устройства для подключений типа "сеть — сеть"</span><span class="sxs-lookup"><span data-stu-id="4d864-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="4d864-178">подключение tooconfigure сайта для сайта, независимо от модели развертывания требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4d864-178">tooconfigure a Site-to-Site connection, regardless of deployment model, you need hello following items:</span></span>

* <span data-ttu-id="4d864-179">VPN-устройство, совместимое с VPN-шлюзами Azure;</span><span class="sxs-lookup"><span data-stu-id="4d864-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="4d864-180">общедоступный IP-адрес IPv4, который находится в пределах NAT.</span><span class="sxs-lookup"><span data-stu-id="4d864-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="4d864-181">Необходимо toohave возможности настройки устройства VPN, или кто-то, позволяет настроить устройство hello для вас.</span><span class="sxs-lookup"><span data-stu-id="4d864-181">You need toohave experience configuring your VPN device, or have someone that can configure hello device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="4d864-182"><a name="forcedtunnel"></a>Вариант маршрутизации с принудительным туннелированием</span><span class="sxs-lookup"><span data-stu-id="4d864-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="4d864-183">Принудительное туннелирование можно настроить для большинства конфигураций.</span><span class="sxs-lookup"><span data-stu-id="4d864-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="4d864-184">Принудительное туннелирование позволяет перенаправлять или «принудительно» все в локальное расположение задней tooyour Интернета трафик через туннель VPN сайт-сайт для проверки и аудита.</span><span class="sxs-lookup"><span data-stu-id="4d864-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="4d864-185">Это критически важное требование безопасности, имеющееся в большинстве корпоративных ИТ-политик.</span><span class="sxs-lookup"><span data-stu-id="4d864-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="4d864-186">Без принудительного туннелирования Интернет-трафик из виртуальных машин в Azure будет всегда проходить из сетевой инфраструктуры Azure непосредственно из toohello Интернета, без параметра tooallow hello вы tooinspect или аудита hello трафика.</span><span class="sxs-lookup"><span data-stu-id="4d864-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="4d864-187">Несанкционированный доступ через Интернет потенциально может привести tooinformation раскрытию или другие виды угроз безопасности.</span><span class="sxs-lookup"><span data-stu-id="4d864-187">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

<span data-ttu-id="4d864-188">Подключение с принудительным туннелированием можно настроить в обеих моделях развертывания с помощью разных средств.</span><span class="sxs-lookup"><span data-stu-id="4d864-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="4d864-189">Дополнительные сведения см. в разделе [Настройка принудительного туннелирования](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="4d864-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="4d864-190">**Схема принудительного туннелирования**</span><span class="sxs-lookup"><span data-stu-id="4d864-190">**Forced tunneling diagram**</span></span>

![Схема принудительного туннелирования VPN-шлюза Azure](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="4d864-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d864-192">Next steps</span></span>

<span data-ttu-id="4d864-193">. В разделе hello [шлюза VPN часто задаваемые вопросы о](vpn-gateway-vpn-faq.md) и [о VPN-шлюз](vpn-gateway-about-vpngateways.md) статей для toohelp Дополнительные сведения вы с вашей разработки.</span><span class="sxs-lookup"><span data-stu-id="4d864-193">See hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information toohelp you with your design.</span></span>

<span data-ttu-id="4d864-194">Дополнительные сведения о конкретных параметрах шлюза см. в разделе [Сведения о параметрах VPN-шлюза](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="4d864-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>