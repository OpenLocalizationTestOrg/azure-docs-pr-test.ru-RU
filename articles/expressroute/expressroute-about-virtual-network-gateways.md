---
title: "шлюзы виртуальной сети ExpressRoute aaaAbout | Документы Microsoft"
description: "Сведения о шлюзах виртуальных сетей ExpressRoute."
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a>Сведения о шлюзах виртуальных сетей ExpressRoute
Шлюз виртуальной сети используется toosend сетевого трафика между виртуальными сетями Azure и расположения в локальной среде. В процессе настройки подключения ExpressRoute необходимо создать и настроить шлюз виртуальной сети и подключение для него.

При создании шлюза виртуальной сети нужно указать несколько параметров. Один из параметров, необходимых hello указывает, будет ли использоваться hello шлюза для ExpressRoute или через виртуальную Частную сеть для трафика. В модели развертывания диспетчера ресурсов hello приветствия равен "-тип шлюза".

При сетевой трафик отправляется на подключение к частной, используется тип шлюза hello «ExpressRoute». Это ссылка tooas шлюз ExpressRoute. Если сетевой трафик отправляется через зашифрованный Здравствуйте общедоступный Интернет, использовать тип шлюза hello «Vpn». Это ссылка tooas VPN-шлюза. При подключениях типа "сеть — сеть", "точка — сеть" и "виртуальная сеть — виртуальная сеть" используется VPN-шлюз.

В виртуальной сети каждому типу шлюза может соответствовать только один шлюз виртуальной сети. Например, у вас может быть только один шлюз виртуальной сети типа VPN и только один типа ExpressRoute. Эта статья посвящена шлюз виртуальной сети hello ExpressRoute.

## <a name="gwsku"></a>SKU шлюзов
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

Если требуется tooupgrade tooa ваш шлюз более мощных шлюза SKU, в большинстве случаев, которые можно использовать hello командлета PowerShell «Изменение размера AzureRmVirtualNetworkGateway». Это будет работать для обновления tooStandard и высокопроизводительные SKU. Тем не менее, toohello tooupgrade UltraPerformance SKU, потребуется шлюз toorecreate hello.

### <a name="aggthroughput"></a>Расчетная суммарная пропускная способность в зависимости от SKU шлюза
Hello следующей таблице показаны типы шлюзов hello и hello предполагаемое суммарную пропускную способность. Эта таблица применяется tooboth hello диспетчера ресурсов и классическое развертывание модели.

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> Пропускная способность приложения зависит от нескольких факторов, таких как задержка начала до конца hello, а номер hello трафика перемещается откроется приложение hello. числа Hello в hello таблицы представляют Привет верхний предел, приложение hello может theorectically достичь в идеальную среду. 
> 
>

## <a name="resources"></a>Интерфейсы REST API и командлеты PowerShell
Дополнительные технические ресурсы и синтаксисе требования при использовании API-интерфейс REST и командлеты PowerShell для настройки шлюза виртуальной сети см. следующие страницы приветствия.

| **Классический** | **Диспетчер ресурсов** |
| --- | --- |
| [PowerShell](https://msdn.microsoft.com/library/mt270335.aspx) |[PowerShell](https://msdn.microsoft.com/library/mt163510.aspx) |
| [ИНТЕРФЕЙС REST API](https://msdn.microsoft.com/library/jj154113.aspx) |[ИНТЕРФЕЙС REST API](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о доступных конфигурациях подключений см. в статье [Технический обзор ExpressRoute](expressroute-introduction.md). 

