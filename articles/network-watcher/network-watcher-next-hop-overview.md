---
title: "Наблюдатель сети Azure прыжке toonext aaaIntroduction | Документы Microsoft"
description: "Эта страница Обзор hello Наблюдатель сети возможность следующего прыжка"
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
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a>Введение toonext участке Наблюдатель сети Azure

Трафик от виртуальной Машины, отправляется tooa назначения, в зависимости от действующих маршрутах hello, связанный с адаптером. Следующий прыжок возвращает тип следующего прыжка hello и IP-адрес пакета из конкретной виртуальной машины и сетевой адаптер. Это помогает toodetermine Если hello пакетов, назначения направленной toohello или является поставщик только трафик hello, черный. Неправильной конфигурации маршрутов пользователем hello, где трафика — расширенный tooan локально или виртуального устройства, можно привести tooconnectivity проблемы. Следующий прыжок также возвращает hello таблицы маршрутов, связанной с hello следующего прыжка. При запросе следующего прыжка, если маршрут hello определяется как маршрут определяемых пользователем, будет возвращаться этого маршрута. В противном случае возвращается системный маршрут.

![Обзор функции определения следующего прыжка][1]

Hello ниже приведен список hello следующего прыжка типов, которые могут быть возвращены при выполнении запроса следующего прыжка.

* Интернет
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

### <a name="next-steps"></a>Дальнейшие действия

Узнайте, как toouse следующего прыжка toofind проблемы с сетевым подключением, посетив [следующего прыжка проверка hello на виртуальной Машине](network-watcher-check-next-hop-portal.md)

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













