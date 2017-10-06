---
title: "Примеры конфигурации маршрутизатора клиента aaaExpressRoute | Документы Microsoft"
description: "Эта страница содержит примеры конфигурации для маршрутизаторов серий Cisco ASA и Juniper MX."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 5c91f24e6082e01c3e8df91b4fcfda46a6c29fa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a><span data-ttu-id="3a954-103">Конфигурация маршрутизатора образцы tooset вверх и управлять маршрутизацией</span><span class="sxs-lookup"><span data-stu-id="3a954-103">Router configuration samples tooset up and manage routing</span></span>
<span data-ttu-id="3a954-104">Эта страница содержит примеры конфигурации интерфейса и маршрутизации для маршрутизаторов серий Cisco IOS-XE и Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="3a954-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="3a954-105">Эти примеры предполагаемого toobe только рекомендации и не должны использоваться как есть.</span><span class="sxs-lookup"><span data-stu-id="3a954-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="3a954-106">Можно работать с вашего поставщика toocome с соответствующие настройки для вашей сети.</span><span class="sxs-lookup"><span data-stu-id="3a954-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3a954-107">Образцы на этой странице, предполагаемой toobe исключительно для рекомендации.</span><span class="sxs-lookup"><span data-stu-id="3a954-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="3a954-108">Необходимо работать с у поставщика продаж / технической группы и вашей сети team toocome вверх с toomeet соответствующие настройки вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="3a954-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="3a954-109">Корпорация Майкрософт не будет поддерживать проблемы связанные tooconfigurations, перечисленные на этой странице.</span><span class="sxs-lookup"><span data-stu-id="3a954-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="3a954-110">Для получения поддержки вам необходимо обратиться к поставщику устройства.</span><span class="sxs-lookup"><span data-stu-id="3a954-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="3a954-111">Параметры MTU и TCP MSS в интерфейсах маршрутизатора</span><span class="sxs-lookup"><span data-stu-id="3a954-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="3a954-112">Hello MTU для интерфейса ExpressRoute hello равно 1500, что hello обычно по умолчанию используется значение MTU для интерфейса Ethernet на маршрутизаторе.</span><span class="sxs-lookup"><span data-stu-id="3a954-112">hello MTU for hello ExpressRoute interface is 1500, which is hello typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="3a954-113">Если маршрутизатор имеет другой MTU по умолчанию, нет toospecify нет необходимости значение на интерфейс маршрутизатора hello.</span><span class="sxs-lookup"><span data-stu-id="3a954-113">Unless your router has a different MTU by default, there is no need toospecify a value on hello router interface.</span></span>
* <span data-ttu-id="3a954-114">В отличие от шлюза VPN Azure hello TCP MSS за канал ExpressRoute toobe указан не требуются.</span><span class="sxs-lookup"><span data-stu-id="3a954-114">Unlike an Azure VPN Gateway, hello TCP MSS for an ExpressRoute circuit does not need toobe specified.</span></span>

<span data-ttu-id="3a954-115">Ниже примеров конфигурации маршрутизатора применяются tooall пиринги.</span><span class="sxs-lookup"><span data-stu-id="3a954-115">Router configuration samples below apply tooall peerings.</span></span> <span data-ttu-id="3a954-116">Для получения дополнительных сведений о маршрутизации обратитесь к статьям [Сеансы пиринга ExpressRoute](expressroute-circuit-peerings.md) и [Требования ExpressRoute к маршрутизации](expressroute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="3a954-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="3a954-117">Маршрутизаторы на основе Cisco IOS-XE</span><span class="sxs-lookup"><span data-stu-id="3a954-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="3a954-118">Hello образцы в этом разделе применяются для любой маршрутизатором, работающим под управлением семейства ОС IOS XE hello.</span><span class="sxs-lookup"><span data-stu-id="3a954-118">hello samples in this section apply for any router running hello IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="3a954-119">1. Настройка интерфейсов и дочерние интерфейсы</span><span class="sxs-lookup"><span data-stu-id="3a954-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="3a954-120">Вам потребуется дочерний интерфейс на пиринг в каждый маршрутизатор подключить tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="3a954-120">You will require a sub interface per peering in every router you connect tooMicrosoft.</span></span> <span data-ttu-id="3a954-121">Дочерний интерфейс можно идентифицировать с помощью идентификатора виртуальной локальной сети или с помощью накопленной пары идентификаторов виртуальных сетей и IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="3a954-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="3a954-122">**Определение интерфейса Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="3a954-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="3a954-123">Этот образец представляет определение интерфейс hello интерфейс с одним идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="3a954-123">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="3a954-124">Hello VLAN ID является уникальным для каждого пиринга.</span><span class="sxs-lookup"><span data-stu-id="3a954-124">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="3a954-125">последний октет Hello IPv4-адрес всегда будет нечетным числом.</span><span class="sxs-lookup"><span data-stu-id="3a954-125">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="3a954-126">**Определение интерфейса QinQ**</span><span class="sxs-lookup"><span data-stu-id="3a954-126">**QinQ interface definition**</span></span>

<span data-ttu-id="3a954-127">Этот образец предоставляет определение интерфейс hello для вложенных интерфейса с помощью двух идентификаторов виртуальных ЛС.</span><span class="sxs-lookup"><span data-stu-id="3a954-127">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="3a954-128">Привет, остается внешней VLAN ID (s тегов), если используется hello же через все пиринги hello.</span><span class="sxs-lookup"><span data-stu-id="3a954-128">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="3a954-129">Hello внутренний идентификатор виртуальной локальной сети (c-tag) уникальным для каждого пиринга.</span><span class="sxs-lookup"><span data-stu-id="3a954-129">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="3a954-130">последний октет Hello IPv4-адрес всегда будет нечетным числом.</span><span class="sxs-lookup"><span data-stu-id="3a954-130">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="3a954-131">2. Настройка сеансов eBGP</span><span class="sxs-lookup"><span data-stu-id="3a954-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="3a954-132">Для каждого пиринга необходимо настроить сеанс BGP с Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3a954-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="3a954-133">Образец Hello ниже включает toosetup сеанс BGP с корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3a954-133">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="3a954-134">Если hello IPv4-адрес, используемый для интерфейса sub a.b.c.d, hello IP-адрес BGP hello окружения (Майкрософт) будет a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="3a954-134">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="3a954-135">последний октет Hello адреса IPv4 соседний узел BGP hello всегда будет четное число.</span><span class="sxs-lookup"><span data-stu-id="3a954-135">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="3a954-136">3. Настройка toobe префиксов, объявленных сеансом BGP hello</span><span class="sxs-lookup"><span data-stu-id="3a954-136">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="3a954-137">Вы можете настроить ваш tooMicrosoft выберите префиксы tooadvertise маршрутизатора.</span><span class="sxs-lookup"><span data-stu-id="3a954-137">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="3a954-138">Это можно сделать с помощью пример "hello".</span><span class="sxs-lookup"><span data-stu-id="3a954-138">You can do so using hello sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="3a954-139">4. Карты маршрутизации</span><span class="sxs-lookup"><span data-stu-id="3a954-139">4. Route maps</span></span>
<span data-ttu-id="3a954-140">Вы можете использовать карты маршрута и префикс перечислены префиксы toofilter распространены в вашей сети.</span><span class="sxs-lookup"><span data-stu-id="3a954-140">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="3a954-141">Можно использовать образец hello ниже tooaccomplish задачу hello.</span><span class="sxs-lookup"><span data-stu-id="3a954-141">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="3a954-142">Убедитесь, что вы задали соответствующие настройки списков префиксов.</span><span class="sxs-lookup"><span data-stu-id="3a954-142">Ensure that you have appropriate prefix lists setup.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="3a954-143">Маршрутизаторы серии Juniper MX</span><span class="sxs-lookup"><span data-stu-id="3a954-143">Juniper MX series routers</span></span>
<span data-ttu-id="3a954-144">Hello образцы в этом разделе применяются для ряда маршрутизаторы Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="3a954-144">hello samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="3a954-145">1. Настройка интерфейсов и дочерние интерфейсы</span><span class="sxs-lookup"><span data-stu-id="3a954-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="3a954-146">**Определение интерфейса Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="3a954-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="3a954-147">Этот образец представляет определение интерфейс hello интерфейс с одним идентификатором виртуальной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="3a954-147">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="3a954-148">Hello VLAN ID является уникальным для каждого пиринга.</span><span class="sxs-lookup"><span data-stu-id="3a954-148">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="3a954-149">последний октет Hello IPv4-адрес всегда будет нечетным числом.</span><span class="sxs-lookup"><span data-stu-id="3a954-149">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


<span data-ttu-id="3a954-150">**Определение интерфейса QinQ**</span><span class="sxs-lookup"><span data-stu-id="3a954-150">**QinQ interface definition**</span></span>

<span data-ttu-id="3a954-151">Этот образец предоставляет определение интерфейс hello для вложенных интерфейса с помощью двух идентификаторов виртуальных ЛС.</span><span class="sxs-lookup"><span data-stu-id="3a954-151">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="3a954-152">Привет, остается внешней VLAN ID (s тегов), если используется hello же через все пиринги hello.</span><span class="sxs-lookup"><span data-stu-id="3a954-152">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="3a954-153">Hello внутренний идентификатор виртуальной локальной сети (c-tag) уникальным для каждого пиринга.</span><span class="sxs-lookup"><span data-stu-id="3a954-153">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="3a954-154">последний октет Hello IPv4-адрес всегда будет нечетным числом.</span><span class="sxs-lookup"><span data-stu-id="3a954-154">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="3a954-155">2. Настройка сеансов eBGP</span><span class="sxs-lookup"><span data-stu-id="3a954-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="3a954-156">Для каждого пиринга необходимо настроить сеанс BGP с Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3a954-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="3a954-157">Образец Hello ниже включает toosetup сеанс BGP с корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3a954-157">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="3a954-158">Если hello IPv4-адрес, используемый для интерфейса sub a.b.c.d, hello IP-адрес BGP hello окружения (Майкрософт) будет a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="3a954-158">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="3a954-159">последний октет Hello адреса IPv4 соседний узел BGP hello всегда будет четное число.</span><span class="sxs-lookup"><span data-stu-id="3a954-159">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="3a954-160">3. Настройка toobe префиксов, объявленных сеансом BGP hello</span><span class="sxs-lookup"><span data-stu-id="3a954-160">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="3a954-161">Вы можете настроить ваш tooMicrosoft выберите префиксы tooadvertise маршрутизатора.</span><span class="sxs-lookup"><span data-stu-id="3a954-161">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="3a954-162">Это можно сделать с помощью пример "hello".</span><span class="sxs-lookup"><span data-stu-id="3a954-162">You can do so using hello sample below.</span></span>

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a><span data-ttu-id="3a954-163">4. Карты маршрутизации</span><span class="sxs-lookup"><span data-stu-id="3a954-163">4. Route maps</span></span>
<span data-ttu-id="3a954-164">Вы можете использовать карты маршрута и префикс перечислены префиксы toofilter распространены в вашей сети.</span><span class="sxs-lookup"><span data-stu-id="3a954-164">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="3a954-165">Можно использовать образец hello ниже tooaccomplish задачу hello.</span><span class="sxs-lookup"><span data-stu-id="3a954-165">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="3a954-166">Убедитесь, что вы задали соответствующие настройки списков префиксов.</span><span class="sxs-lookup"><span data-stu-id="3a954-166">Ensure that you have appropriate prefix lists setup.</span></span>

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a><span data-ttu-id="3a954-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3a954-167">Next Steps</span></span>
<span data-ttu-id="3a954-168">В разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="3a954-168">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

