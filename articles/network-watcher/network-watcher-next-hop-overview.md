---
title: "Общие сведения о функции определения следующего прыжка в Наблюдателе за сетями Azure | Документация Майкрософт"
description: "Эта страница содержит общие сведения о функции определения следующего прыжка в Наблюдателе за сетями."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5dd65d2418cae206965a13013dd990b916ad0733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-next-hop-in-azure-network-watcher"></a>Общие сведения о функции определения следующего прыжка в Наблюдателе за сетями Azure

Трафик из виртуальной машины отправляется по назначению в зависимости от действующих маршрутов, связанных с сетевой картой. Функция определения следующего прыжка возвращает тип следующего прыжка и IP-адрес пакета из определенной виртуальной машины и сетевой карты. Это позволяет определить, направляется ли пакет по назначению или трафик передается в "черную дыру". Неправильная настройка маршрутов пользователем, при которой трафик направляется в локальное расположение или на виртуальное устройство, может привести к проблемам подключения. Функция определения следующего прыжка также возвращает таблицу маршрутов, связанную со следующим прыжком. Если при запросе следующего прыжка маршрут задан как определяемый пользователем, то возвращается этот маршрут. В противном случае возвращается системный маршрут.

![Обзор функции определения следующего прыжка][1]

Ниже приведен список типов следующего прыжка, которые могут быть возвращены при запросе следующего прыжка.

* Интернет
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

### <a name="next-steps"></a>Дальнейшие действия

Узнайте, как использовать функцию определения следующего прыжка для поиска проблем с сетевыми подключениями, ознакомившись с разделом [Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal](network-watcher-check-next-hop-portal.md) (Определение типа следующего прыжка с помощью функции определения следующего прыжка в Наблюдателе за сетями на портале).

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













