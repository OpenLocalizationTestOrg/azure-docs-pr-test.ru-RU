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
ms.openlocfilehash: 0ebc3ef4a64432e993dd6ed69766bb64544fe433
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="1602d-103">Планирование и проектирование VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="1602d-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="1602d-104">Планирование и проектирование конфигураций распределенных подключений и подключений между виртуальными сетями может быть очень простым или достаточно сложным в зависимости от потребностей сети.</span><span class="sxs-lookup"><span data-stu-id="1602d-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="1602d-105">В этой статье рассматриваются основные вопросы планирования и проектирования.</span><span class="sxs-lookup"><span data-stu-id="1602d-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="1602d-106"><a name="planning"></a>Планирование</span><span class="sxs-lookup"><span data-stu-id="1602d-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="1602d-107"><a name="compare"></a>Возможности распределенного подключения</span><span class="sxs-lookup"><span data-stu-id="1602d-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="1602d-108">Если вам требуется безопасное подключение локальных сайтов к виртуальной сети, доступны три варианта: подключение типа "сеть — сеть", подключение типа "точка — сеть" и канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1602d-108">If you want to connect your on-premises sites securely to a virtual network, you have three different ways to do so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="1602d-109">Сравните различные доступные варианты подключений между организациями.</span><span class="sxs-lookup"><span data-stu-id="1602d-109">Compare the different cross-premises connections that are available.</span></span> <span data-ttu-id="1602d-110">На выбор влияют различные факторы, в том числе следующие.</span><span class="sxs-lookup"><span data-stu-id="1602d-110">The option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="1602d-111">Какая пропускная способность требуется для решения?</span><span class="sxs-lookup"><span data-stu-id="1602d-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="1602d-112">Вы хотите обмениваться данными через общедоступный Интернет по безопасному VPN-подключению или через частное подключение?</span><span class="sxs-lookup"><span data-stu-id="1602d-112">Do you want to communicate over the public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="1602d-113">У вас есть общедоступный IP-адрес, который можно использовать?</span><span class="sxs-lookup"><span data-stu-id="1602d-113">Do you have a public IP address available to use?</span></span>
* <span data-ttu-id="1602d-114">Вы планируете использовать VPN-устройство?</span><span class="sxs-lookup"><span data-stu-id="1602d-114">Are you planning to use a VPN device?</span></span> <span data-ttu-id="1602d-115">Если да, является ли оно совместимым?</span><span class="sxs-lookup"><span data-stu-id="1602d-115">If so, is it compatible?</span></span>
* <span data-ttu-id="1602d-116">Вы подключаете лишь несколько компьютеров или требуется постоянное подключения для сайта?</span><span class="sxs-lookup"><span data-stu-id="1602d-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="1602d-117">Какой тип VPN-шлюза необходим для решения, которое вы хотите создать?</span><span class="sxs-lookup"><span data-stu-id="1602d-117">What type of VPN gateway is required for the solution you want to create?</span></span>
* <span data-ttu-id="1602d-118">Какой номер SKU шлюза следует использовать?</span><span class="sxs-lookup"><span data-stu-id="1602d-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="1602d-119"><a name="planningtable"></a>Таблица планирования</span><span class="sxs-lookup"><span data-stu-id="1602d-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="1602d-120">Приведенная ниже таблица поможет вам подобрать наилучший вариант подключения для решения.</span><span class="sxs-lookup"><span data-stu-id="1602d-120">The following table can help you decide the best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="1602d-121"><a name="gwsku"></a>SKU шлюзов</span><span class="sxs-lookup"><span data-stu-id="1602d-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="1602d-122"><a name="wf"></a>Рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="1602d-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="1602d-123">Ниже приведен стандартный рабочий процесс для настройки облачных подключений.</span><span class="sxs-lookup"><span data-stu-id="1602d-123">The following list outlines the common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="1602d-124">Спроектируйте и спланируйте топологию подключений и составьте список адресных пространств для всех сетей, которые необходимо подключить.</span><span class="sxs-lookup"><span data-stu-id="1602d-124">Design and plan your connectivity topology and list the address spaces for all networks you want to connect.</span></span>
2. <span data-ttu-id="1602d-125">Создайте виртуальную сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="1602d-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="1602d-126">Создайте VPN-шлюз для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="1602d-126">Create a VPN gateway for the virtual network.</span></span>
4. <span data-ttu-id="1602d-127">Создайте и настройте подключения к локальным сетям или другим виртуальным сетям (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="1602d-127">Create and configure connections to on-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="1602d-128">Создайте и настройте подключение "точка — сеть" для VPN-шлюза Azure (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="1602d-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="1602d-129"><a name="design"></a>Проектирование</span><span class="sxs-lookup"><span data-stu-id="1602d-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="1602d-130"><a name="topologies"></a>Топологии подключений</span><span class="sxs-lookup"><span data-stu-id="1602d-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="1602d-131">Начните с просмотра схем в статье о [Основные сведения о VPN-шлюзах Azure](vpn-gateway-about-vpngateways.md) .</span><span class="sxs-lookup"><span data-stu-id="1602d-131">Start by looking at the diagrams in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="1602d-132">В этой статье содержатся базовые схемы, а также описаны модели развертывания для каждой топологии и доступные инструменты развертывания, которыми можно воспользоваться для развертывания конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1602d-132">The article contains basic diagrams, the deployment models for each topology, and the available deployment tools you can use to deploy your configuration.</span></span>

### <span data-ttu-id="1602d-133"><a name="designbasics"></a>Основы проектирования</span><span class="sxs-lookup"><span data-stu-id="1602d-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="1602d-134">В следующих разделах представлены основные сведения о VPN-шлюзе.</span><span class="sxs-lookup"><span data-stu-id="1602d-134">The following sections discuss the VPN gateway basics.</span></span> 

#### <span data-ttu-id="1602d-135"><a name="servicelimits"></a>Ограничения сетевых служб</span><span class="sxs-lookup"><span data-stu-id="1602d-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="1602d-136">Прокрутите таблицы для просмотра [ограничений сетевых служб](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="1602d-136">Scroll through the tables to view [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="1602d-137">Эти ограничения могут повлиять на проектирование.</span><span class="sxs-lookup"><span data-stu-id="1602d-137">The limits listed may impact your design.</span></span>

#### <span data-ttu-id="1602d-138"><a name="subnets"></a>О подсетях</span><span class="sxs-lookup"><span data-stu-id="1602d-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="1602d-139">При создании подключений необходимо определить диапазоны адресов подсетей.</span><span class="sxs-lookup"><span data-stu-id="1602d-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="1602d-140">Нельзя, чтобы они перекрывались.</span><span class="sxs-lookup"><span data-stu-id="1602d-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="1602d-141">Перекрывающаяся подсеть — это подсеть, в которой одна виртуальная сеть или локальное расположение находится в том же адресном пространстве, что и другое расположение.</span><span class="sxs-lookup"><span data-stu-id="1602d-141">An overlapping subnet is when one virtual network or on-premises location contains the same address space that the other location contains.</span></span> <span data-ttu-id="1602d-142">Это значит, что ваши сетевые инженеры должны выделить для ваших локальных сетей диапазон, который будет использоваться для подсетей и пространства IP-адресов Azure.</span><span class="sxs-lookup"><span data-stu-id="1602d-142">This means that you need your network engineers for your local on-premises networks to carve out a range for you to use for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="1602d-143">Это адресное пространство не должно использоваться в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="1602d-143">You need address space that is not being used on the local on-premises network.</span></span>

<span data-ttu-id="1602d-144">Перекрытие подсетей также следует предотвратить при работе с подключениями между виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="1602d-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="1602d-145">Если подсети перекрываются и какой-либо IP-адрес существует в виртуальных сетях отправки и назначения, то создать подключение между виртуальными сетями не удастся.</span><span class="sxs-lookup"><span data-stu-id="1602d-145">If your subnets overlap and an IP address exists in both the sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="1602d-146">Azure не сможет перенаправить данные в другую виртуальную сеть, так как адрес назначения является частью виртуальной сети отправки.</span><span class="sxs-lookup"><span data-stu-id="1602d-146">Azure can't route the data to the other VNet because the destination address is part of the sending VNet.</span></span>

<span data-ttu-id="1602d-147">Для работы VPN-шлюзов требуется специальная подсеть, которая называется подсетью шлюза.</span><span class="sxs-lookup"><span data-stu-id="1602d-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="1602d-148">Чтобы подсети шлюзов работали надлежащим образом, каждую из них нужно назвать GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="1602d-148">All gateway subnets must be named GatewaySubnet to work properly.</span></span> <span data-ttu-id="1602d-149">Убедитесь, что для подсети шлюза не используется другое имя. Кроме того, не следует развертывать в ней виртуальные машины или что-либо другое.</span><span class="sxs-lookup"><span data-stu-id="1602d-149">Be sure not to name your gateway subnet a different name, and don't deploy VMs or anything else to the gateway subnet.</span></span> <span data-ttu-id="1602d-150">Ознакомьтесь с [подсетями шлюза](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="1602d-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="1602d-151"><a name="local"></a>О локальных сетевых шлюзах</span><span class="sxs-lookup"><span data-stu-id="1602d-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="1602d-152">Обычно термин "шлюз локальной сети" означает локальное расположение.</span><span class="sxs-lookup"><span data-stu-id="1602d-152">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="1602d-153">В классической модели развертывания локальный сетевой шлюз называется сайтом локальной сети.</span><span class="sxs-lookup"><span data-stu-id="1602d-153">In the classic deployment model, the local network gateway is referred to as a Local Network Site.</span></span> <span data-ttu-id="1602d-154">При настройке локального сетевого шлюза для него нужно задать имя, общедоступный IP-адрес локального VPN-устройства и префиксы адресов, принадлежащих к локальному расположению.</span><span class="sxs-lookup"><span data-stu-id="1602d-154">When you configure a local network gateway, you give it a name, specify the public IP address of the on-premises VPN device, and specify the address prefixes that are in the on-premises location.</span></span> <span data-ttu-id="1602d-155">Azure проверяет наличие сетевого трафика по префиксам адресов назначения, учитывает конфигурацию, указанную для локального сетевого шлюза, и соответствующим образом направляет пакеты.</span><span class="sxs-lookup"><span data-stu-id="1602d-155">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for the local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="1602d-156">При необходимости эти префиксы адресов можно изменить.</span><span class="sxs-lookup"><span data-stu-id="1602d-156">You can modify the address prefixes as needed.</span></span> <span data-ttu-id="1602d-157">Дополнительные сведения см. в статье [Шлюзы локальной сети](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="1602d-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="1602d-158"><a name="gwtype"></a>О типах шлюзов</span><span class="sxs-lookup"><span data-stu-id="1602d-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="1602d-159">Для топологии чрезвычайно важен правильный выбор типа шлюза.</span><span class="sxs-lookup"><span data-stu-id="1602d-159">Selecting the correct gateway type for your topology is critical.</span></span> <span data-ttu-id="1602d-160">Шлюз не будет работать надлежащим образом, если выбран неправильный тип.</span><span class="sxs-lookup"><span data-stu-id="1602d-160">If you select the wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="1602d-161">По типу шлюза определяется, как подключается шлюз. Это обязательный параметр конфигурации для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1602d-161">The gateway type specifies how the gateway itself connects and is a required configuration setting for the Resource Manager deployment model.</span></span>

<span data-ttu-id="1602d-162">Существуют такие типы шлюзов:</span><span class="sxs-lookup"><span data-stu-id="1602d-162">The gateway types are:</span></span>

* <span data-ttu-id="1602d-163">Vpn</span><span class="sxs-lookup"><span data-stu-id="1602d-163">Vpn</span></span>
* <span data-ttu-id="1602d-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1602d-164">ExpressRoute</span></span>

#### <span data-ttu-id="1602d-165"><a name="connectiontype"></a>О типах подключений</span><span class="sxs-lookup"><span data-stu-id="1602d-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="1602d-166">Для каждой конфигурации необходим конкретный тип подключения.</span><span class="sxs-lookup"><span data-stu-id="1602d-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="1602d-167">Существуют такие типы подключения:</span><span class="sxs-lookup"><span data-stu-id="1602d-167">The connection types are:</span></span>

* <span data-ttu-id="1602d-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="1602d-168">IPsec</span></span>
* <span data-ttu-id="1602d-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="1602d-169">Vnet2Vnet</span></span>
* <span data-ttu-id="1602d-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1602d-170">ExpressRoute</span></span>
* <span data-ttu-id="1602d-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="1602d-171">VPNClient</span></span>

#### <span data-ttu-id="1602d-172"><a name="vpntype"></a>О типах VPN</span><span class="sxs-lookup"><span data-stu-id="1602d-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="1602d-173">Для каждой конфигурации нужен определенный тип VPN.</span><span class="sxs-lookup"><span data-stu-id="1602d-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="1602d-174">Если необходимо совместить две конфигурации, например создать подключения типа "сеть — сеть" и "точка — сеть" в одной виртуальной сети, нужно указать тип VPN, который отвечает требованиям обоих подключений.</span><span class="sxs-lookup"><span data-stu-id="1602d-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection to the same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="1602d-175">В приведенных ниже таблицах приведены типы VPN и соответствующие конфигурации подключений.</span><span class="sxs-lookup"><span data-stu-id="1602d-175">The following tables show the VPN type as it maps to each connection configuration.</span></span> <span data-ttu-id="1602d-176">Тип VPN для шлюза должен соответствовать конфигурации, которую требуется создать.</span><span class="sxs-lookup"><span data-stu-id="1602d-176">Make sure the VPN type for your gateway matches the configuration that you want to create.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="1602d-177"><a name="devices"></a>VPN-устройства для подключений типа "сеть — сеть"</span><span class="sxs-lookup"><span data-stu-id="1602d-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="1602d-178">Независимо от модели развертывания для настройки подключения типа "сеть — сеть" необходимы следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="1602d-178">To configure a Site-to-Site connection, regardless of deployment model, you need the following items:</span></span>

* <span data-ttu-id="1602d-179">VPN-устройство, совместимое с VPN-шлюзами Azure;</span><span class="sxs-lookup"><span data-stu-id="1602d-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="1602d-180">общедоступный IP-адрес IPv4, который находится в пределах NAT.</span><span class="sxs-lookup"><span data-stu-id="1602d-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="1602d-181">Необходимо иметь опыт настройки VPN-устройства или возможность обратиться к специалисту, который может настроить устройство для вас.</span><span class="sxs-lookup"><span data-stu-id="1602d-181">You need to have experience configuring your VPN device, or have someone that can configure the device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="1602d-182"><a name="forcedtunnel"></a>Вариант маршрутизации с принудительным туннелированием</span><span class="sxs-lookup"><span data-stu-id="1602d-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="1602d-183">Принудительное туннелирование можно настроить для большинства конфигураций.</span><span class="sxs-lookup"><span data-stu-id="1602d-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="1602d-184">Оно позволяет перенаправлять или "принудительно направлять" весь Интернет-трафик обратно в локальное расположение через VPN типа "сеть — сеть" для проверки и аудита.</span><span class="sxs-lookup"><span data-stu-id="1602d-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="1602d-185">Это критически важное требование безопасности, имеющееся в большинстве корпоративных ИТ-политик.</span><span class="sxs-lookup"><span data-stu-id="1602d-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="1602d-186">Без принудительного туннелирования Интернет-трафик из виртуальных машин в Azure будет всегда поступать из инфраструктуры сети Azure непосредственно в Интернет, без возможности его проверки или аудита.</span><span class="sxs-lookup"><span data-stu-id="1602d-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="1602d-187">Неавторизованный доступ в Интернет может привести к раскрытию информации или другим нарушениям безопасности.</span><span class="sxs-lookup"><span data-stu-id="1602d-187">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

<span data-ttu-id="1602d-188">Подключение с принудительным туннелированием можно настроить в обеих моделях развертывания с помощью разных средств.</span><span class="sxs-lookup"><span data-stu-id="1602d-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="1602d-189">Дополнительные сведения см. в разделе [Настройка принудительного туннелирования](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="1602d-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="1602d-190">**Схема принудительного туннелирования**</span><span class="sxs-lookup"><span data-stu-id="1602d-190">**Forced tunneling diagram**</span></span>

![Схема принудительного туннелирования VPN-шлюза Azure](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="1602d-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1602d-192">Next steps</span></span>

<span data-ttu-id="1602d-193">Дополнительные сведения о проектировании см. в статьях [VPN-шлюз: вопросы и ответы](vpn-gateway-vpn-faq.md) и [Шлюзы VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="1602d-193">See the [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information to help you with your design.</span></span>

<span data-ttu-id="1602d-194">Дополнительные сведения о конкретных параметрах шлюза см. в разделе [Сведения о параметрах VPN-шлюза](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="1602d-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>