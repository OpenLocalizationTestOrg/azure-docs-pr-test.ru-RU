---
title: "Примеры конфигурации маршрутизатора клиента ExpressRoute | Документация Майкрософт"
description: "Эта страница содержит примеры конфигурации для маршрутизаторов серий Cisco ASA и Juniper MX."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: d6ea716f-d5ee-4a61-92b0-640d6e7d6974
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 83a7da2db537a3c900e90432455d59e8ac56d917
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="router-configuration-samples-to-set-up-and-manage-nat"></a><span data-ttu-id="78f58-103">Примеры конфигурации маршрутизатора для настройки и управления NAT</span><span class="sxs-lookup"><span data-stu-id="78f58-103">Router configuration samples to set up and manage NAT</span></span>
<span data-ttu-id="78f58-104">Эта страница содержит примеры конфигурации NAT для маршрутизаторов серий Cisco ASA и Juniper SRX.</span><span class="sxs-lookup"><span data-stu-id="78f58-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="78f58-105">Эти примеры имеют только справочный характер и не должны использоваться как есть.</span><span class="sxs-lookup"><span data-stu-id="78f58-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="78f58-106">Подходящие конфигурации для своей сети можно выработать совместно с поставщиком.</span><span class="sxs-lookup"><span data-stu-id="78f58-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="78f58-107">Примеры на этой странице имеют исключительно справочный характер.</span><span class="sxs-lookup"><span data-stu-id="78f58-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="78f58-108">Для получения подходящей конфигурации, которая удовлетворяет вашим потребностям, необходимо провести совместную работу со специалистами по продажам или техническими специалистами поставщика и вашими сетевыми специалистами.</span><span class="sxs-lookup"><span data-stu-id="78f58-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="78f58-109">Корпорация Майкрософт не предоставляет поддержки по вопросам, связанным с конфигурациями, перечисленными на этой странице.</span><span class="sxs-lookup"><span data-stu-id="78f58-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="78f58-110">Для получения поддержки вам необходимо обратиться к поставщику устройства.</span><span class="sxs-lookup"><span data-stu-id="78f58-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="78f58-111">Примеры конфигурации маршрутизатора относятся к пирингам Azure Public и Microsoft.</span><span class="sxs-lookup"><span data-stu-id="78f58-111">Router configuration samples below apply to Azure Public and Microsoft peerings.</span></span> <span data-ttu-id="78f58-112">Вы не должны настраивать NAT для частного пиринга Azure.</span><span class="sxs-lookup"><span data-stu-id="78f58-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="78f58-113">Для получения дополнительных сведений обратитесь к статьям [Сеансы пиринга ExpressRoute](expressroute-circuit-peerings.md) и [Требования ExpressRoute к NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="78f58-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="78f58-114">Для подключений к Интернету и ExpressRoute ДОЛЖНЫ использоваться отдельные пулы IP-адресов NAT.</span><span class="sxs-lookup"><span data-stu-id="78f58-114">You MUST use separate NAT IP pools for connectivity to the internet and ExpressRoute.</span></span> <span data-ttu-id="78f58-115">Использование одного пула IP-адресов NAT для подключения к Интернету и ExpressRoute приведет к асимметричной маршрутизации и потере подключения.</span><span class="sxs-lookup"><span data-stu-id="78f58-115">Using the same NAT IP pool across the internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="78f58-116">Брандмауэры Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="78f58-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-to-microsoft"></a><span data-ttu-id="78f58-117">Конфигурация NAT для трафика от сети клиента в Майкрософт</span><span class="sxs-lookup"><span data-stu-id="78f58-117">PAT configuration for traffic from customer network to Microsoft</span></span>
    object network MSFT-PAT
      range <SNAT-START-IP> <SNAT-END-IP>


    object-group network MSFT-Range
      network-object <IP> <Subnet_Mask>

    object-group network on-prem-range-1
      network-object <IP> <Subnet-Mask>

    object-group network on-prem-range-2
      network-object <IP> <Subnet-Mask>

    object-group network on-prem
      network-object object on-prem-range-1
      network-object object on-prem-range-2

    nat (outside,inside) source dynamic on-prem pat-pool MSFT-PAT destination static MSFT-Range MSFT-Range

### <a name="pat-configuration-for-traffic-from-microsoft-to-customer-network"></a><span data-ttu-id="78f58-118">Конфигурация PAT для трафика из Майкрософт в клиентскую сеть</span><span class="sxs-lookup"><span data-stu-id="78f58-118">PAT configuration for traffic from Microsoft to customer network</span></span>

<span data-ttu-id="78f58-119">**Интерфейсы и направление:**</span><span class="sxs-lookup"><span data-stu-id="78f58-119">**Interfaces and Direction:**</span></span>

    Source Interface (where the traffic enters the ASA): inside
    Destination Interface (where the traffic exits the ASA): outside

<span data-ttu-id="78f58-120">**Конфигурация:**</span><span class="sxs-lookup"><span data-stu-id="78f58-120">**Configuration:**</span></span>

<span data-ttu-id="78f58-121">Пул преобразования сетевых адресов:</span><span class="sxs-lookup"><span data-stu-id="78f58-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="78f58-122">Целевой сервер:</span><span class="sxs-lookup"><span data-stu-id="78f58-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="78f58-123">Группа объектов для клиентских IP-адресов</span><span class="sxs-lookup"><span data-stu-id="78f58-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="78f58-124">Команды преобразования сетевых адресов:</span><span class="sxs-lookup"><span data-stu-id="78f58-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="78f58-125">Маршрутизаторы серии Juniper SRX</span><span class="sxs-lookup"><span data-stu-id="78f58-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-the-cluster"></a><span data-ttu-id="78f58-126">1. Создайте избыточные интерфейсы Ethernet для кластера.</span><span class="sxs-lookup"><span data-stu-id="78f58-126">1. Create redundant Ethernet interfaces for the cluster</span></span>
    interfaces {
        reth0 {
            description "To Internal Network";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 1;
            }
            unit 100 {
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
        reth1 {
            description "To Microsoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "To Microsoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a><span data-ttu-id="78f58-127">2. Создайте две зоны безопасности.</span><span class="sxs-lookup"><span data-stu-id="78f58-127">2. Create two security zones</span></span>
* <span data-ttu-id="78f58-128">Доверенная зона предназначена для внутренней сети, а недоверенная зона — для внешней сети, направленной на граничные маршрутизаторы.</span><span class="sxs-lookup"><span data-stu-id="78f58-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="78f58-129">Назначьте соответствующие интерфейсы зонам.</span><span class="sxs-lookup"><span data-stu-id="78f58-129">Assign appropriate interfaces to the zones</span></span>
* <span data-ttu-id="78f58-130">Включите службы для интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="78f58-130">Allow services on the interfaces</span></span>

    <span data-ttu-id="78f58-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="78f58-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="78f58-132">3. Создайте политики безопасности между зонами.</span><span class="sxs-lookup"><span data-stu-id="78f58-132">3. Create security policies between zones</span></span>
    security {
        policies {
            from-zone Trust to-zone Untrust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
            from-zone Untrust to-zone Trust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
        }
    }


### <a name="4-configure-nat-policies"></a><span data-ttu-id="78f58-133">4. Настройте политики NAT.</span><span class="sxs-lookup"><span data-stu-id="78f58-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="78f58-134">Создайте два пула NAT.</span><span class="sxs-lookup"><span data-stu-id="78f58-134">Create two NAT pools.</span></span> <span data-ttu-id="78f58-135">Один будет использоваться для исходящего трафика NAT в Майкрософт, а второй — для трафика от Майкрософт клиенту.</span><span class="sxs-lookup"><span data-stu-id="78f58-135">One will be used to NAT traffic outbound to Microsoft and other from Microsoft to the customer.</span></span>
* <span data-ttu-id="78f58-136">Создайте правила для преобразования сетевых адресов соответствующего трафика.</span><span class="sxs-lookup"><span data-stu-id="78f58-136">Create rules to NAT the respective traffic</span></span>
  
       security {
           nat {
               source {
                   pool SNAT-To-ExpressRoute {
                       routing-instance {
                           External-ExpressRoute;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   pool SNAT-From-ExpressRoute {
                       routing-instance {
                           Internal;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   rule-set Outbound_NAT {
                       from routing-instance Internal;
                       to routing-instance External-ExpressRoute;
                       rule SNAT-Out {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-To-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
                   rule-set Inbound-NAT {
                       from routing-instance External-ExpressRoute;
                       to routing-instance Internal;
                       rule SNAT-In {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-From-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
               }
           }
       }

### <a name="5-configure-bgp-to-advertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="78f58-137">5. Настройки BGP для использования выборочных префиксов в каждом направлении</span><span class="sxs-lookup"><span data-stu-id="78f58-137">5. Configure BGP to advertise selective prefixes in each direction</span></span>
<span data-ttu-id="78f58-138">Обратитесь к примерам на странице [Примеры настройки маршрутизации ](expressroute-config-samples-routing.md) .</span><span class="sxs-lookup"><span data-stu-id="78f58-138">Refer to samples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="78f58-139">6. Создайте политики.</span><span class="sxs-lookup"><span data-stu-id="78f58-139">6. Create policies</span></span>
    routing-options {
                  autonomous-system <Customer-ASN>;
    }
    policy-options {
        prefix-list Microsoft-Prefixes {
            <IP-Address/Subnet-Mask;
            <IP-Address/Subnet-Mask;
        }
        prefix-list private-ranges {
            10.0.0.0/8;
            172.16.0.0/12;
            192.168.0.0/16;
            100.64.0.0/10;
        }
        policy-statement Advertise-NAT-Pools {
            from {
                protocol static;
                route-filter <NAT-Pool-Address/Subnet-mask> prefix-length-range /32-/32;
            }
            then accept;
        }
        policy-statement Accept-from-Microsoft {
            term 1 {
                from {
                    instance External-ExpressRoute;
                    prefix-list-filter Microsoft-Prefixes orlonger;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
        policy-statement Accept-from-Internal {
            term no-private {
                from {
                    instance Internal;
                    prefix-list-filter private-ranges orlonger;
                }
                then reject;
            }
            term bgp {
                from {
                    instance Internal;
                    protocol bgp;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
    }
    routing-instances {
        Internal {
            instance-type virtual-router;
            interface reth0.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Microsoft;
            }
            protocols {
                bgp {
                    group customer {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-ASN-1>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
        External-ExpressRoute {
            instance-type virtual-router;
            interface reth1.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Internal;
            }
            protocols {
                bgp {
                    group edge-router {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-Public-ASN>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
    }

## <a name="next-steps"></a><span data-ttu-id="78f58-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78f58-140">Next steps</span></span>
<span data-ttu-id="78f58-141">Дополнительные сведения см. в разделе [Вопросы и ответы по ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="78f58-141">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

