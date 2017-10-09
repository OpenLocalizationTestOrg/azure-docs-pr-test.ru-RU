---
title: "Примеры конфигурации маршрутизатора клиента aaaExpressRoute | Документы Microsoft"
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
ms.openlocfilehash: b5faca0666bda6173e54abb0b6560d5f8bf8bfc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a><span data-ttu-id="8da78-103">Конфигурация маршрутизатора образцы tooset вверх и управлять NAT</span><span class="sxs-lookup"><span data-stu-id="8da78-103">Router configuration samples tooset up and manage NAT</span></span>
<span data-ttu-id="8da78-104">Эта страница содержит примеры конфигурации NAT для маршрутизаторов серий Cisco ASA и Juniper SRX.</span><span class="sxs-lookup"><span data-stu-id="8da78-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="8da78-105">Эти примеры предполагаемого toobe только рекомендации и не должны использоваться как есть.</span><span class="sxs-lookup"><span data-stu-id="8da78-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="8da78-106">Можно работать с вашего поставщика toocome с соответствующие настройки для вашей сети.</span><span class="sxs-lookup"><span data-stu-id="8da78-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8da78-107">Образцы на этой странице, предполагаемой toobe исключительно для рекомендации.</span><span class="sxs-lookup"><span data-stu-id="8da78-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="8da78-108">Необходимо работать с у поставщика продаж / технической группы и вашей сети team toocome вверх с toomeet соответствующие настройки вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="8da78-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="8da78-109">Корпорация Майкрософт не будет поддерживать проблемы связанные tooconfigurations, перечисленные на этой странице.</span><span class="sxs-lookup"><span data-stu-id="8da78-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="8da78-110">Для получения поддержки вам необходимо обратиться к поставщику устройства.</span><span class="sxs-lookup"><span data-stu-id="8da78-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="8da78-111">Ниже примеров конфигурации маршрутизатора применяются tooAzure пиринги Public и Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="8da78-111">Router configuration samples below apply tooAzure Public and Microsoft peerings.</span></span> <span data-ttu-id="8da78-112">Вы не должны настраивать NAT для частного пиринга Azure.</span><span class="sxs-lookup"><span data-stu-id="8da78-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="8da78-113">Для получения дополнительных сведений обратитесь к статьям [Сеансы пиринга ExpressRoute](expressroute-circuit-peerings.md) и [Требования ExpressRoute к NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="8da78-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="8da78-114">НЕОБХОДИМО использовать отдельные пулы NAT IP для toohello подключения к Интернету и ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8da78-114">You MUST use separate NAT IP pools for connectivity toohello internet and ExpressRoute.</span></span> <span data-ttu-id="8da78-115">С помощью hello пул же NAT IP между hello Интернета и приведет к ExpressRoute асимметричного маршрутизации и потери связи.</span><span class="sxs-lookup"><span data-stu-id="8da78-115">Using hello same NAT IP pool across hello internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="8da78-116">Брандмауэры Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="8da78-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a><span data-ttu-id="8da78-117">МАРИЯ конфигурации для входящего трафика с tooMicrosoft сети клиента</span><span class="sxs-lookup"><span data-stu-id="8da78-117">PAT configuration for traffic from customer network tooMicrosoft</span></span>
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

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a><span data-ttu-id="8da78-118">МАРИЯ конфигурации для трафика сети toocustomer Microsoft</span><span class="sxs-lookup"><span data-stu-id="8da78-118">PAT configuration for traffic from Microsoft toocustomer network</span></span>

<span data-ttu-id="8da78-119">**Интерфейсы и направление:**</span><span class="sxs-lookup"><span data-stu-id="8da78-119">**Interfaces and Direction:**</span></span>

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

<span data-ttu-id="8da78-120">**Конфигурация:**</span><span class="sxs-lookup"><span data-stu-id="8da78-120">**Configuration:**</span></span>

<span data-ttu-id="8da78-121">Пул преобразования сетевых адресов:</span><span class="sxs-lookup"><span data-stu-id="8da78-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="8da78-122">Целевой сервер:</span><span class="sxs-lookup"><span data-stu-id="8da78-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="8da78-123">Группа объектов для клиентских IP-адресов</span><span class="sxs-lookup"><span data-stu-id="8da78-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="8da78-124">Команды преобразования сетевых адресов:</span><span class="sxs-lookup"><span data-stu-id="8da78-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="8da78-125">Маршрутизаторы серии Juniper SRX</span><span class="sxs-lookup"><span data-stu-id="8da78-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a><span data-ttu-id="8da78-126">1. Создание избыточных интерфейсов Ethernet для кластера hello</span><span class="sxs-lookup"><span data-stu-id="8da78-126">1. Create redundant Ethernet interfaces for hello cluster</span></span>
    interfaces {
        reth0 {
            description "tooInternal Network";
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
            description "tooMicrosoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "tooMicrosoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a><span data-ttu-id="8da78-127">2. Создайте две зоны безопасности.</span><span class="sxs-lookup"><span data-stu-id="8da78-127">2. Create two security zones</span></span>
* <span data-ttu-id="8da78-128">Доверенная зона предназначена для внутренней сети, а недоверенная зона — для внешней сети, направленной на граничные маршрутизаторы.</span><span class="sxs-lookup"><span data-stu-id="8da78-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="8da78-129">Назначьте соответствующие интерфейсы toohello зоны</span><span class="sxs-lookup"><span data-stu-id="8da78-129">Assign appropriate interfaces toohello zones</span></span>
* <span data-ttu-id="8da78-130">Разрешить службам в интерфейсах hello</span><span class="sxs-lookup"><span data-stu-id="8da78-130">Allow services on hello interfaces</span></span>

    <span data-ttu-id="8da78-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="8da78-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="8da78-132">3. Создайте политики безопасности между зонами.</span><span class="sxs-lookup"><span data-stu-id="8da78-132">3. Create security policies between zones</span></span>
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


### <a name="4-configure-nat-policies"></a><span data-ttu-id="8da78-133">4. Настройте политики NAT.</span><span class="sxs-lookup"><span data-stu-id="8da78-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="8da78-134">Создайте два пула NAT.</span><span class="sxs-lookup"><span data-stu-id="8da78-134">Create two NAT pools.</span></span> <span data-ttu-id="8da78-135">Один будет tooMicrosoft исходящего трафика используется tooNAT и других toohello клиентов Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8da78-135">One will be used tooNAT traffic outbound tooMicrosoft and other from Microsoft toohello customer.</span></span>
* <span data-ttu-id="8da78-136">Создание правил трафика соответствующих tooNAT hello</span><span class="sxs-lookup"><span data-stu-id="8da78-136">Create rules tooNAT hello respective traffic</span></span>
  
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
                       toorouting-instance External-ExpressRoute;
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
                       toorouting-instance Internal;
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

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="8da78-137">5. Настройка BGP tooadvertise Выборочный префиксы в каждом направлении</span><span class="sxs-lookup"><span data-stu-id="8da78-137">5. Configure BGP tooadvertise selective prefixes in each direction</span></span>
<span data-ttu-id="8da78-138">Ссылки toosamples в [образцы настройки маршрутизации ](expressroute-config-samples-routing.md) страницы.</span><span class="sxs-lookup"><span data-stu-id="8da78-138">Refer toosamples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="8da78-139">6. Создайте политики.</span><span class="sxs-lookup"><span data-stu-id="8da78-139">6. Create policies</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="8da78-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8da78-140">Next steps</span></span>
<span data-ttu-id="8da78-141">В разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="8da78-141">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

