---
title: "aaaAzure и обзор сети виртуальных Машин Linux | Документы Microsoft"
description: "Общие сведения о виртуальных сетях в Azure и Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Azure и Linux: обзор сетей виртуальных машин
## <a name="virtual-networks"></a>Виртуальные сети
Azure виртуальной сети (VNet) — это представление сети в облаке hello. Это логическое изоляции hello подписки tooyour выделенное облако Azure. Кроме того, можно полностью настраивать hello блоки IP-адресов, параметры DNS, политики безопасности и таблицы маршрутов в этой сети. Кроме того, вы можете дополнительно разделить виртуальную сеть на подсети и запускать виртуальные машины Azure IaaS и (или) облачные службы (экземпляры роли PaaS). Кроме того можно подключить hello виртуальной сети tooyour локальной сети с помощью одного из hello возможности подключения, доступные в Azure. По сути вы можете развернуть tooAzure вашей сети, с полный контроль над блоки IP-адресов с преимуществами hello корпоративного уровня, предоставляемые Azure.

* [Обзор виртуальной сети](../../virtual-network/virtual-networks-overview.md)

toocreate виртуальной сети с помощью hello Azure CLI, перейдите сюда, toofollow hello пошагово.

* [Как toocreate виртуальной сети с помощью hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>группы сетевой безопасности;
Группы безопасности сети (NSG) содержит список правил список управления доступом (ACL), которые разрешают или запрещают трафик tooyour экземпляров виртуальных Машин в виртуальной сети. Группы безопасности сети можно связать с подсетями или отдельными экземплярами виртуальных машин в одной из подсетей. Когда NSG связана с подсетью, правила ACL hello применяются tooall экземпляров виртуальных Машин hello в этой подсети. Кроме того, tooan трафик отдельных виртуальных Машин может быть ограничен продолжается связывание NSG непосредственно toothat виртуальной Машины.

* [Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md)
* [Как Nsg toocreate в hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>Определяемые пользователем маршруты
При добавлении виртуальных машин (ВМ) tooa виртуальной сети (VNet) в Azure, вы заметите hello виртуальные машины, может toocommunicate друг с другом по сети hello автоматически. Необязательно toospecify шлюз, даже если hello виртуальные машины находятся в разных подсетях. Hello то же верно для обмена данными между toohello ВМ hello общедоступный Интернет и даже tooyour в локальной сети, когда владельцем гибридного подключения из Azure tooyour присутствует центра обработки данных.

* [Что такое определяемые пользователем маршруты и IP-пересылка?](../../virtual-network/virtual-networks-udr-overview.md)
* [Создание UDR в hello Azure CLI](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a>Связывание tooyour полное доменное имя виртуальной Машины с Linux
При создании виртуальной машины (VM) в hello портал Azure с помощью модели развертывания диспетчера ресурсов hello, общедоступный IP-адрес ресурса для hello виртуальной машины создается автоматически. Можно использовать этот IP адрес tooremotely доступа hello виртуальной Машины. Несмотря на то, что портал hello не создает полное доменное имя или полное доменное имя, по умолчанию, можно добавить один после создания виртуальной Машины hello.

* [Создание полного доменного имени в hello портал Azure](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>Сетевые интерфейсы
Сетевого интерфейса (NIC) является hello взаимосвязь между виртуальной машины (VM) и hello базового сетевого программного обеспечения. В этой статье описываются сетевой интерфейс, и как она используется в модели развертывания диспетчера ресурсов Azure hello.

* [Virtual Network Interfaces](../../virtual-network/virtual-network-network-interface.md) (Виртуальные сетевые интерфейсы)

## <a name="virtual-nics-and-dns-labeling"></a>Виртуальные сетевые карты и DNS-метки
При наличии сервера, что необходима toobe постоянно, но этот сервер считается скот рабочий и уничтожения и часто развернута, вы будете toouse DNS метки на имя сетевого Адаптера toopersist hello на hello виртуальной сети.  С hello, следуя руководство по настроит постоянно именованный сетевого Адаптера с статический IP-адрес.

* [Создать полную среду Linux с помощью hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>Шлюзы виртуальной сети
Шлюз виртуальной сети используется toosend сетевого трафика между виртуальными сетями Azure и расположения в локальной среде, а также между виртуальными сетями в Azure (VNet-VNet). При настройке шлюза VPN необходимо создать и настроить шлюз виртуальной сети и подключение для него.

* [Основные сведения о VPN-шлюзах Azure](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>Внутренняя балансировка нагрузки
Azure Load Balancer является балансировщиком нагрузки 4-го уровня (TCP, UDP). Подсистема балансировки нагрузки Hello обеспечивает высокую доступность путем распределения входящего трафика между экземплярами службы работоспособности в облачных службах или виртуальных машин в набор балансировки нагрузки. Azure Load Balancer может также представить данные службы на нескольких портах, нескольких IP-адресах или обоими этими способами.

* [Создание внутренней подсистемы балансировки нагрузки с помощью hello Azure CLI](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

