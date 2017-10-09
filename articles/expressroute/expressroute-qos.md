---
title: "Требования к ExpressRoute aaaQoS | Документы Microsoft"
description: "На этой странице подробно описаны требования по настройке качества обслуживания для каналов ExpressRoute и управлению им."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a>Требования к качеству обслуживания для ExpressRoute
В Skype для бизнеса имеются различные рабочие нагрузки, требующие дифференцированного подхода к качеству обслуживания. Если планируется tooconsume голоса службы с помощью ExpressRoute, необходимо придерживаться toohello требованиям, описанным ниже.

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> Требования к QoS применяются toohello только пиринг Майкрософт. значения DSCP Hello в вашей сетевой трафик, поступающий на Azure для общедоступного пиринга и открытого пиринга Azure будут too0 сброса. 
> 
> 

Hello следующей таблице приведен список маркировку DSCP, используемые Скайп для бизнеса. См. слишком[управление QoS для Скайп для бизнеса](https://technet.microsoft.com/library/gg405409.aspx) для получения дополнительной информации.

| **Класс трафика** | **Обработка (пометки DSCP)** | **Рабочие нагрузки Skype для бизнеса** |
| --- | --- | --- |
| **Голосовая связь** |EF (46) |Голосовая связь Skype и Lync |
| **Интерактивный** |AF41 (34) |Видео, VBSS |
| AF21 (18) |Совместный доступ к приложениям | |
| **По умолчанию** |AF11 (10) |Передача файлов |
| CS0 (0) |Другие варианты | |

* Необходимо классифицировать hello рабочих нагрузок и пометить правильные значения DSCP hello. Следуйте инструкциям, hello [здесь](https://technet.microsoft.com/library/gg405409.aspx) о том, как tooset маркировки DSCP в сети.
* Вам необходимо настроить и поддерживать несколько очередей качества обслуживания в сети. Голосовой должно быть автономный класс и подвергаются обработке EF hello, указанные в RFC 3246. 
* Можно решить, hello очереди механизм перегрузки политику обнаружения и распределение пропускной способности каждого класса трафика. Но hello пометки DSCP для Скайп для решения бизнес-задач, которые необходимо сохранить. Если вы используете маркировки DSCP, не перечисленные выше, например AF31 (26), необходимо переписать это too0 значение DSCP перед отправкой пакета tooMicrosoft hello. Корпорация Майкрософт только отправляет пакеты, отмеченные hello значение DSCP, показанное в hello над таблицей. 

## <a name="next-steps"></a>Дальнейшие действия
* См. требования к toohello для [маршрутизации](expressroute-routing.md) и [NAT](expressroute-nat.md).
* См. следующие hello ссылки tooconfigure подключение ExpressRoute.
  
  * [Создание канала ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Настройка маршрутизации](expressroute-howto-routing-classic.md)
  * [Связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-classic.md)

