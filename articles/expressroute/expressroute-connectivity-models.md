---
title: "Модели подключения к ExpressRoute: подключение через поставщиков сетевых услуг, обмен и поставщики Ethernet tooMicrosoft Azure | Документы Microsoft"
description: "Данная статья содержит различные режимы hello связи между сетью и службами Microsoft Azure, Office 365 и Dynamics 365 hello клиента. Клиенты могут использовать поставщиков MPLS, поставщиков облачных служб Exchange и поставщиков Ethernet."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: cherylmc
ms.openlocfilehash: 2682e6e45b2892869068f132bedb4bb08e3f89a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-connectivity-models"></a>Модели подключения ExpressRoute
Можно создать соединение между локальной сетью и hello Microsoft cloud тремя разными способами [совместного размещения CloudExchange](#CloudExchange), [Ethernet-подключение точка-точка](#Ethernet)и [Подключения any к any (IPVPN)](#IPVPN). Поставщики услуг подключения могут предлагать одну или несколько моделей подключения. Можно работать с моделью hello toopick подключения поставщика, лучше всего подходит для вас.
<br><br>

![Схема моделей подключения ExpressRoute](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <a name="CloudExchange"></a>Совместное размещение в Cloud Exchange
Если настроить совместное размещение на территории с exchange облака, вы можете упорядочить toohello виртуального кросс подключений Microsoft cloud через Ethernet exchange hello совместного размещения поставщика. Совместное размещение поставщики обеспечивают уровня 2 кросс подключений или управляемый сервер уровня 3 кросс подключений между инфраструктуры на территории совместного размещения hello и облако Microsoft hello.

## <a name="Ethernet"></a>Подключения Ethernet типа "точка — точка"
Можно подключить вашей локальной центрах обработки данных и офисов toohello Microsoft cloud через Ethernet ссылки между узлами. Точка-точка Ethernet поставщики могут предложить подключений уровня 2 или управляемого подключения уровня 3 между сайтом и hello Microsoft cloud.

## <a name="IPVPN"></a>Сети типа "любой к любому" (IPVPN)
Можно интегрировать hello Microsoft cloud глобальной сети. Поставщики IP VPN (обычно это MPLS VPN) предлагают подключение между филиалами и центрами обработки данных типа "любой к любому". облако может быть глобальной сети toomake взаимосвязанных tooyour она выглядеть просто Microsoft Hello, например филиала компании. Обычно поставщики глобальных вычислительных сетей предлагают управляемые подключения третьего уровня. ExpressRoute и функции по всем hello выше модели подключения к идентичны. 

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше о подключениях ExpressRoute и доменах маршрутизации. См. статью [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).
* Узнайте о функциях ExpressRoute. В разделе hello [Технический обзор ExpressRoute](expressroute-introduction.md)
* Найти поставщика услуг. См. статью [Партнеры и одноранговые расположения ExpressRoute](expressroute-locations.md).
* Убедитесь, что выполнены все необходимые условия. См. статью [Предварительные требования и контрольный список для ExpressRoute](expressroute-prerequisites.md).
* См. требования к toohello для [маршрутизации](expressroute-routing.md), [NAT](expressroute-nat.md), и [QoS](expressroute-qos.md).
* Настройте подключение ExpressRoute.
  * [Создайте канал ExpressRoute.](expressroute-howto-circuit-portal-resource-manager.md)
  * [Настройка маршрутизации](expressroute-howto-routing-portal-resource-manager.md)
  * [Связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md)
